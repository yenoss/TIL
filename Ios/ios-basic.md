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

## REF.
[textfield highlight](https://coderwall.com/p/kir4kw/moving-to-the-next-uitextfield-in-an-ios-app)