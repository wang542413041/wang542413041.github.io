---
layout: post
---

# 逃逸闭包：
闭包作为参数传入函数，闭包在函数返回后才执行，该闭包为逃逸闭包；

使用 @escaping 修饰,表明闭包允许逃逸，如果想在外部使用参数闭包，则需要使用该关键字进行标记，否则会有编译错误
 
不使用 @escaping，还想再外部捕获会报编译错误
转化非逃逸参数到泛型参数需要允许它逃逸，即使用 @escaping 标记
 
逃逸方法：
1. 将闭包保存在函数外部定义的变量中
 
注意：
1. 逃逸闭包需要显示的使用self，因为后续闭包还要执行，使用self增加引用计数，防止被调用的时候被杀死
2. 非逃逸闭包可以隐式引用self

```swift
var completionHandlers: [() -> String] = [] // @escaping
func someFuncionWithEscapingClosure(completionHandler: @escaping () -> String) {
    completionHandlers.append(completionHandler)
}
```