---
layout: post
---

# swift 错误处理

## 错误定义

```
enum XXXError: Error {
    case invalidSelection
    case outOfStock
}

// 抛出错误
throw XXXError.outOfStock
```

## 错误抛出函数

只有抛出函数才能传递错误

```
func canThrowErrors() throws -> String {
    if (1 == 1) {
        throw XXXError.invalidSelection
    }
}
``` 

## 处理错误

### do-catch 处理错误

```
do {
    print("执行函数")
    try canThrowErrors()
} catch {
    print(error)
}
```

### try? 可选错误

计算表达式，如果表达式抛出错误，则x为nil。通常可以和`if let``guard let`使用

`let x = try? canThrowErrors()`

### try! 禁用错误

在确认不方法不会在运行时抛出错误使用；

如果实际抛出错误，则在运行时收到错误。

`let x = try! canThrowErrors()`

### defer 清理操作

您可以使用defer语句在代码执行离开当前代码块之前执行一组语句。

无论执行如何离开当前代码块，该语句都可以让您执行任何必要的清理——无论它是因为抛出错误还是因为诸如returnor之类的语句而离开break。

例如，您可以使用defer语句来确保关闭文件描述符并释放手动分配的内存。

```
func processFile(fileName: String) throws {
    let file = open(fileName)
    defer { // 会在函数执行完毕后清理
        close(file)
    }
}
```