# -RealtekHD-audiodg.exe-
挖矿病毒利用RealtekHD声卡文件，生成audiodg.exe木马文件的解决方法
前言
首先大家会打开到这篇文章，就已经说明你大概率已经被病毒所困扰了。自从byrut网站为大家提供了大部分不安全的盗版游戏资源，很多人都从这些资源中被病毒感染，并且难以靠普通的杀毒软件进行杀毒了。其中一个最让人最难受的资源，就是这个类似病毒工厂会自动生成木马一样的病毒。如果你想靠自己处理掉这些木马文件，或许我的文章所分享的经验可以帮助到你！

我并非专业查杀病毒的人员，只是一个普通的本科开发实习生，以下内容是为了简单的分享一下这类病毒的手动清理方式，还有分享发现这一病毒后的思考，以及溯源的方式与思路。如果你还没能删除这恶心难缠的挖矿木马病毒，希望你读完我的文章之后，可以靠自己揪出这一病毒，收获自己满满的成就感！
以下让我详细说来从发现病毒、到删除病毒的全过程与思考！





正文
实际上所有的木马病毒其实都已经走在了杀毒软件的前沿，或者是已经理解了杀毒软件的特效，并且利用其特性进行伪装、隐藏的病毒。想要避免被其中的挖矿病毒迫害，其实我们可以很简单的靠自己进行排查。

一、首先打开你的任务管理器

莫名的内存占用，已经可以说明你的电脑资源正在被木马程序利用，挖矿木马会悄无声息的耗费你的资源，并且难以利用杀毒软件进行查杀与溯源。如果你不能排除哪个进程是异常的，那你可以自己通过搜索引擎去搜素一下那些异常启动的进程，不过这大概率不能马上排查出你的病毒所在。
无论是挖矿病毒，还是窃取个人资料的木马病毒，只要跑起来，一定会占用你内存与CPU性能资源，这时你就要有自己发现异常进程、文件的能力。你可以简单的依靠杀毒软件进行侦查与入手。
我所了解到的一个挖矿病毒，会不断的在你的C盘temp临时缓存文件夹内不断的生成木马文件‘audiodg.exe’。你想要通过temp文件夹溯源是不可行的，因为temp文件夹是系统存放各种临时文件的位置，无论是内行还是外行人员，都没办法轻易的对temp文件夹内产生的文件进行溯源！
但是这一简单的生成木马操作，很容易被你的普通杀毒软件所侦查到。生成的exe文件必定会被相应的进程所启用，这一动作是会被杀毒软件所记录的，这就是你从一个文件揪出整个病毒程序路径的关键突破口！

二、对执行木马文件的进程进行简单了解
主动运行audiodg.exe文件的进程是名为taskhost.exe一个进程。taskhost.exe进程是Windows7/8/8.1/10自带的一个进程，是负责Windows运行计划的，简单的来说也可以称作计划任务程序。病毒利用系统的特性去自启自身生成的木马程序，从而避开杀毒软件的检测与阻拦。Audiodg.exe文件是Windows音频设备图形隔离程序，一般路径是固定的，一旦出现在其他位置就必定是木马程序所伪装的，会被轻易的查杀。但我们可以顺着这一文件往下继续查找，可以揪出taskhost.exe这一进程，禁用taskhost 的网络后，禁用声卡驱动，可以暂时避免系统主动运行木马文件，暂缓你的电脑风险。
继续深入taskhost的文件路径，你会发现名为RealtekHD文件夹下的taskhost.exe文件是不可见的，即便是开启隐藏文件查看的情况下也是不可见的。病毒程序已经悄悄的修改了你的RealtekHD程序，随着你的声卡驱动程序的运行，病毒程序也会乘机不断的在你开机的时候生成木马文件到Windowstask或者temp文件夹中，每次开机就会生成一个木马在你的C盘中，可谓是恶心至极。
这时候就是你抉择的时候了，是选择同归于尽，重装操作系统彻底消灭这一病毒，还是壮士断腕，砍掉自己的声音系统文件？好汉当然是要留得青山在，不怕没柴烧吧！我们通过U盘启动盘进入到PE系统，进入到系统路径：“C：\ProgramData\RealtelHD”直接删除掉此文件夹，系统会提示你此文件为系统文件，不建议你删除！没有办法的是，我们为了根绝这一挖矿木马，只能把它的宿主也给干掉了。
删除此文件夹后重启，会导致你的系统声音异常，也不是声卡驱动错误，通过市面上的驱动管家进行修复也是无济于事。各类修复声音的方法也不可行！因为问题并非出现在声卡驱动与硬件上。
病毒的问题解决了，但是系统的声音要怎么恢复？用电脑自带的疑难解答？这个问题经过我的长时间研究，无论是重装声卡驱动，复制其他正常的系统文件过来，统统都不能恢复你的系统声音。就算是进行系统升级，也不一定能够解决这一现象。就连接上耳机的情况也是无声的。
问题出在系统文件上，就要通过检查系统完整性进行处理。利用系统文件检查器(sfc.exe)。系统文件检查器(sfc.exe) 是 windows 内置的工具,用于验证系统文件完整性并修复损坏的系统文件。使用CMD命令窗口运行一下代码 ：命令1“DISM.exe /Online /Cleanup-image /Restorehealth”   
命令2“sfc /scannow”
完成此操作后，你会发现系统声音神奇的恢复了！哈哈恭喜你！

