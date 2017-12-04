# 主要记录go语言精彩片段

判断是否panic，如果panic了就返回false，如果没有就返回true。
并且我们要知道这个函数的运用 其实也就是recover()的运用 go运行时会从恐慌变成正常运行。原因就是在
if中调用了recover函数了。
```go
/判断是否是panic
func OrPanic(f func()) bool {
	defer func ()  {
		if n := recover(); n != nil {
			return true
		}
	}()
	f()
	return false
}
```
