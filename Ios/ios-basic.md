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
## REF.
[textfield highlight](https://coderwall.com/p/kir4kw/moving-to-the-next-uitextfield-in-an-ios-app)

[add imageBoarder](https://stackoverflow.com/questions/34984966/rounding-uiimage-and-adding-a-border)