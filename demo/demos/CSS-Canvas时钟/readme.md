Canvas动效时钟-萌萌哒的小球到处跑,带定时、计时，夜间模式，控制面板。主要是萌-20160625-

update 20160626
把定时、计时补全了。 再补了下控制面板 增加夜间模式…… 还有逻辑 交互 一大堆。挖的坑全填完了。
主要时间都花在隐性的交互上了吧，Go按钮交互还是不太满意。
傻逼似的把倒计时的年也做进去了…… 藏起来就当个彩蛋吧。
这个应该是目前做的最完美的Html了吧。
…………………………

函数预留可改倒计时等 萌萌哒做做提字板的彩蛋最好了

计时器进了个坑，本想节约资源，定时器中判断时间过1s后才渲染背景时间，期间只渲染掉落的小球，后来才想起。如果不逐帧清理画布，小球满天飞了…… 还好坑不深，只是出坑后的JS结构方面看起来有点别扭。


还有个坑，如果页面未激活，chrome应该是有定时器的省电策略。再切回会瞬间一大堆小球。
我猜这个机制应该是切回后台即冷冻，类似iPhone APP后台机制，切回后快进 达到正常时刻/次数的定时器效果。但是集中的运算会产生大量的小球。
解决办法：在清理数组函数中增加最大小球数目可破。这样就算集中计算N次定时器也只有那么多小球--