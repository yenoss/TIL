# Ios-basic

## WHAT?
+ ios에 대한 이야기를 적습니다.

## 1. textField keybaord에서 return을 눌렀을경우 다음 textfield로 넘어가기.

+ 사용자의 편의성을 위해 특정 필드를 입력한 다음 return키를 눌러 옆에 있는 다음 필드로 넘기고 싶었다.

```
if textField == field01 {
    textField.resignFirstResponder()
    self.field02.becomeFirstResponder()

} else if textField == field02 {
    textField.resignFirstResponder()
    self.field03.becomeFirstResponder()
}
.
.
.

```

+ 간단히 return을 눌렀을경우 현재 입력필드를 resign시키고 다음필드에 becomeFristResponder 함수를 써주면된다.


## 2. ios Default Indecator
+ ios에서 자주 쓰이는 기본 indicator를 돌려보자


```
        
        let actInd: UIActivityIndicatorView = UIActivityIndicatorView()
        actInd.frame = CGRect.init(x: 0.0, y: 0.0, width: 40.0, height: 40.0)
        actInd.center = self.view.center
        actInd.hidesWhenStopped = true
        actInd.activityIndicatorViewStyle = .whiteLarge        
        self.view.addSubview(actInd)
        actInd.startAnimating()
		actInt.stopAnimating()
```


## 3. UIImage에 border를 추가해보자.
+ image뷰 자체에 border를 추가하여 새로운 이미지를 만들어보자.



```
extension UIImage {
    func imageWithBorder(width: CGFloat, color: UIColor) -> UIImage? {
        let square = CGSize(width: min(size.width, size.height) + width * 2, height: min(size.width, size.height) + width * 2)
        let imageView = UIImageView(frame: CGRect(origin: CGPoint(x: 0, y: 0), size: square))
        imageView.contentMode = .Center
        imageView.image = self
        imageView.layer.masksToBounds = true
        imageView.layer.borderWidth = width
        imageView.layer.borderColor = color.CGColor
        UIGraphicsBeginImageContextWithOptions(imageView.bounds.size, false, scale)
        guard let context = UIGraphicsGetCurrentContext() else { return nil }
        imageView.layer.renderInContext(context)
        let result = UIGraphicsGetImageFromCurrentImageContext()
        UIGraphicsEndImageContext()
        return result
    }
}
```

## 4. Lauch Image Asset
+ xcode에서 launch image를 설정한는 방법중에 대표적으로 프로젝트 생성시 생겨나는 launchscreen stroyboard를 사용하는 방법과 launch image asset을 이용하는 방법이있다.
+ 두 개중  하나를 설정해서 써야하는데, launch ScreenImage를 사용할경우 
 	+ target>project App Icons and LaunchImages에서 LaunchScreenFile을 해당 스토리보드로 설정해주면 사용할 수 있고,
 	+ asset을 이용하는 경우는  App Icons ans LaunchImages에서 Launch ImageSource에 asset을 설정해준다음.. 꼭!! LaunchScreenFile에  아무것도 없는 빈곳으로 놓아야 해당 asset으로 Launch 이미지가 보여진다.
 	+ 추가로, 만일 기존앱이 최초에 LaunchScreenFile로 빌드되어있다면,  꼭 앱을 삭제하고  다시 실행해야, 다시 설정한 asset으로 Launch화면이 바뀔것이다. 

## 5. Screenshot Detection
+ 내앱에서 스크린샷을 찍는 것을 감지하고 싶다면 아래와 같은 코드를 사용하면 된다
 
```
let mainQueue = OperationQueue.main
        NotificationCenter.default.addObserver(forName: NSNotification.Name.UIApplicationUserDidTakeScreenshot,
                                                                object: nil,
                                                                queue: mainQueue) { notification in
                                                                    print("screee!!!")
        }
```


## REF.
[textfield highlight](https://coderwall.com/p/kir4kw/moving-to-the-next-uitextfield-in-an-ios-app)

[add imageBoarder](https://stackoverflow.com/questions/34984966/rounding-uiimage-and-adding-a-border)

[screenshot detection](http://www.ios-blog.co.uk/tutorials/objective-c/how-to-detect-screenshots-in-objective-c-and-swift-like-snapchat/)