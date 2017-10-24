# Go by Example: Timers

我们经常在将来的某个时间点来执行某段代码，或者在一定间隔不停地执行某段代码。 Go 内置的 timer 和 ticker
能使得这个变得很容易

```go
package main

import (
	"time"	
	"fmt"
)

func main() {
	timer1 := time.NewTimer(time.Second)

	// 阻塞，直到 1秒钟后，从 channel C 中接收到值
	<-time1.C
	fmt.Println("Timer 1 is expired")

	// 使用Timer 比 time.Sleep 的好处是你能在计时器到期之前，取消计时器
	time2 := time.NewTimer(time.Second)
	go func(){
		<-timer2.C  // 在 time2 还没有被到期之前，它就被停止了
		fmt.Println("Timer 2 expired")
	}()

	stop2 := time2.Stop() //停止计时器，返回值可以判断计时器是到期了，还是被stop了
	//如果此次调用停止了timer，则返回true，如果已经到期或者已经被停止了返回 false
	if stop2 {
		fmt.Println("Timer 2 stopped")
	}//否则已经到期了
}
```
