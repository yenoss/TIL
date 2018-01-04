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

## 6. ViewDidLayoutSbuviews
+ 뷰컨트롤러의 뷰가 자식뷰를 배치하고 난뒤에 호출되는 메소드. 즉 뷰가 세팅된 후 변경 할것이 필요하다면 여시서 수정.
+ stroybaord상에서 설정한 view의 속성값을 변경을 하고싶다면 이곳에서 콜해야한다.
+ 필자는 button에 Round효과를 주기위해 viewdidlayoutsubview안에 라운드 코드를 추가하였다.

```
    override func viewDidLayoutSubviews() {
        btn.layer.cornerRadius = btnDefault01.frame.width/2
}
```

## 7. IOS Archive error
+ ios 테스트플라잇 배포를 위해 archive를 하고 itunse 에 upload를 하려하였으나 아래와 같은 에러가 발생

```
 1. itunse store operation Failed 
    Description length:25523232
```

+ archive 파일 => show PackageContents => Products => Applications =>  show PackageContents => Info.plist를 수정

+ info.plist에 DTXcodeBuild 를 9C40으로 수정. 
+ 필자는 xcode 9.1을 사용하고있는데 현재 버전의 버그라고한다.

## 8. ERROR ITMS-90475: "Invalid Bundle. iPad Multitasking support requires launch storyboard in bundle 'com.companyname.appname.'"

+ 앱의 status bar를 false를 하고 archiving 후 appstore에 올리려하였으나 위와같은 에러로 좌절(?) 되었다.
+ 이유는 문구에 나와있듯 multitasking이 지원되는 앱에서 어떻게 앱을 보여줄거냐 에대한 이야기이고, 필자의 서비스는 항상 풀스크린으로 지원할것임으로 아래와 같이 세팅한다

+ General > requireds full screen 

+ 언제든 full screen으로 사용하는 것으로 에러가 해결되었다.

## 9. Sticker app Error
+  This iMessage application is missing its required iMessage app extension, 
+  위와 같은 에러가 발생하면, xcode에서 imessage extension의 타켓의 development target이 알맞은지 확인해보면된다.

## REF.
[textfield highlight](https://coderwall.com/p/kir4kw/moving-to-the-next-uitextfield-in-an-ios-app)

[add imageBoarder](https://stackoverflow.com/questions/34984966/rounding-uiimage-and-adding-a-border)

[screenshot detection](http://www.ios-blog.co.uk/tutorials/objective-c/how-to-detect-screenshots-in-objective-c-and-swift-like-snapchat/)

[btn round](https://stackoverflow.com/questions/37770456/how-to-make-uibutton-a-circle)

[layoutsubview](https://developer.apple.com/documentation/uikit/uiviewcontroller/1621398-viewdidlayoutsubviews)

[xcode archive](https://stackoverflow.com/questions/47644270/xcode-9-2-upload-to-app-store-fails-with-description-length-and-invalid-toolchai)

[err-fullscreen](https://stackoverflow.com/questions/32557783/invalid-bundle-error-requires-launch-storyboard)

[err-sticker](https://stackoverflow.com/questions/40332947/imessage-application-is-missing-its-required-imessage-app-extension-can-not-ru)