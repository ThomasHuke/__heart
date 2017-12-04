# 主要记录go语言精彩片段

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
