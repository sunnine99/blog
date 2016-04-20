---
layout: post
title:  "2016读书笔记之《奇特的一生》part two"
date:   2016-01-02 21:46:11 +0300
categories: blog
---
Saturday, January 2, 2016 3:48 PM

柳比歇夫的时间统计法在大多数人看来，是一件非常琐碎无聊又耗时间的事情。抛开平时随时随地记录不说，每次总结还要花很多时间。柳比歇夫也记录下了总结耗费的时间，详细的每月小结一般要一个半到三个小时，再加上一个小时来制定下个月的计划。年度总结耗费的时间久更多了，一般是十七八个小时，要花几天的功夫。

得益于信息时代的发展，50年后的今天，我们有很多很多可以帮助我们提高效率的工具，让生活变得更轻松。我个人感受最深的要算是各种云端服务，比如我所有的文件都放到dropbox里，这样不管是在家还是在办公室，不管是手机上还是电脑上，都可以随时随地处理文件，而不用拿着U盘或者移动硬盘拷来拷去；我的邮件也是可以在任意的终端来收取和回复；我看过不错的网页文章我也会放到pocket里面，随时可以重温；我的日记和写的文章全在Evernote里面，这全都是基于云端而不是本地的应用，而且都是超越系统的，不管是windows，还是OSX，或是android或IOS，有些做得好的软件甚至在Linux下面都没有问题，比如dropbox。

不过，正如我在part one里写的，这本奇书并没有对西方世界产生影响，所以我暂时还没找到专门的软件来进行时间统计。我只能依靠outlook的calendar功能加上excel的pivot table来实现，还算方便。下面是细节。

在outlook的calendar里面用鼠标选中时间区域，就可以建立一个appointment。

![时间统计法]({{ site.baseurl }}/image/outlook1.png)

软件里每个小时被分成了四部分，最小区域是15分钟，也可以手动改成任何时间段，但这样做效率就比较低了，所以我的最小时间段就是15分钟，每次鼠标一点就可以选中15分钟的整数倍区域。

![时间统计法]({{ site.baseurl }}/image/outlook2.png)

这样就很比较容易记录下自己做的每一件事情，花费的时间。

![时间统计法]({{ site.baseurl }}/image/outlook3.png)

光是记下来是不够的，我们需要很方便的统计出来我们每一项活动花了多少时间。这个就得利用calendar的category功能了，这个功能好像我就在outlook里发现有，其他的calendar类似google calendar就没有category的功能，只能放弃。在每个活动上右键就可以看到category的选项

![时间统计法]({{ site.baseurl }}/image/outlook4.png)

但问题是你得先建立起各种category，根据你的各种活动，划分为不同的类别。一般记录两周，就大致知道自己平时都会做些什么事，然后就得开始制定不同的类别。category分的越细，以后的统计数据就越详尽。比如我的category就分成了八个大类，每一大类用了不同的颜色，然后每一个大类里还有为数不等的小类，比如说体育方面，我就分成了三类，以后如果还有别的运动项目，比如跑步，就再增加一项Sports_Running，这里用了下划线也是很关键，之后我介绍统计时会细说，下划线前面是大类别，后面是小类别。

![时间统计法]({{ site.baseurl }}/image/outlook5.png)

建立好了category，每一项活动都会归属到某一个类别里，这样calendar就变得五颜六色了

![时间统计法]({{ site.baseurl }}/image/outlook6.png)

记录一段时间后需要统计了，这时就得把calendar的数据导出来，步骤如下，之前的步骤可以在OSX下的outlook里，也可以在windows的outlook里，但导出这一步，必须在windows下才能完成

![时间统计法]({{ site.baseurl }}/image/outlook7.png)

![时间统计法]({{ site.baseurl }}/image/outlook8.png)

![时间统计法]({{ site.baseurl }}/image/outlook9.png)

"export to a file”，必须是”comma separated values”，然后选”calendar”，选择日期范围

![时间统计法]({{ site.baseurl }}/image/outlook10.png)

![时间统计法]({{ site.baseurl }}/image/outlook11.png)

得到一个xxx.csv的文件，然后用excel打开，可以看到所有的活动都在表里，但是真正有意义的，只有起始时间和category！可以将其他的column都删掉。

![时间统计法]({{ site.baseurl }}/image/excel1.png)

这个时候，我们需要增加一栏duration，因为原始数据里只有起始时间和结束时间，我们得调用函数自己算出这项活动花费的时间。
调用的函数为：=(D2+E2-B2-C2)x24
之所以要×24，是因为默认的单位是天！×24就变成小时了。

然后因为我的category里设置了大类（category名称里下划线之前的部分），我还需要增加一栏，调用字符串函数来切割下划线，获得下划线前面的字符串
函数为：=LEFT(F2,FIND(\"\_\",F2)-1)，F栏必须是category
细节就不解释了。

最后我还想获得每一周的统计结果，所以我还增加了一栏显示周数，函数为：=WEEKNUM(B2,1)，B栏必须是start date
如果是把周一当成每周开始的话，函数改成：=WEEKNUM(B2,2)，括号后面为1表示把周日当成每周的开始。

增加完这几项，我们就可以得到这样的数据了，比如这个活动，从3PM到3:45PM，所以花了45分钟，duration就是0.75个小时，小类别是Work_Admin，大类别是Work，这是第53周的活动。

![时间统计法]({{ site.baseurl }}/image/excel2.png)

然后我们就要用到excel强大的pivot table功能了，选中所有数据，然后”insert” “pivot table"

![时间统计法]({{ site.baseurl }}/image/excel3.png)

create pivot table，点“OK”

![时间统计法]({{ site.baseurl }}/image/excel4.png)

excel里会出现一个新的sheet，但什么都没有，我们需要编辑我们需要的数据。把”category"拖到”rows”，把”duration”拖到”values”里

![时间统计法]({{ site.baseurl }}/image/excel5.png)

然后编辑”values”里面的”value field settings"

![时间统计法]({{ site.baseurl }}/image/excel6.png)

选中”sum"

![时间统计法]({{ site.baseurl }}/image/excel7.png)

这样我们就可以得到一个统计表格了，我们每一类活动耗费了多少时间，就一清二楚了。

![时间统计法]({{ site.baseurl }}/image/excel8.png)

但是我们想看到每周的数据，只需要将”week”拖到”filter”里

![时间统计法]({{ site.baseurl }}/image/excel9.png)

然后统计表上方就会出现”week”的选项，选择某一周（也可以多选）

![时间统计法]({{ site.baseurl }}/image/excel10.png)

就得到了第52周的数据
![时间统计法]({{ site.baseurl }}/image/excel11.png)

因为我是连睡觉时间都统计了，所以每周的24×7=168小时全部都会出现在统计表里。这样看不直观，可以按照耗费的时间多少排一下序，

![时间统计法]({{ site.baseurl }}/image/excel12.png)

![时间统计法]({{ site.baseurl }}/image/excel13.png)


按duration求和的降序排列，这样耗费时间最多的类别就会出现在上面，毫无悬念肯定是睡觉用的时间最多啊，每天接近8个小时的睡眠，应该还比较健康:)

![时间统计法]({{ site.baseurl }}/image/excel14.png)

还可以计算每一类占的时间百分比，在”value”里增加一项，然后选成”% of grand total"

![时间统计法]({{ site.baseurl }}/image/excel15.png)


就可以得到百分比了，睡觉占了三分之一啊，排第二的是工作中的行政事务，所以说这一周的破事实在太多了……

![时间统计法]({{ site.baseurl }}/image/excel16.png)

这是按小类别分的，我们不是有大类别么，重新建一个pivot table，将”cate”拖入"rows"

![时间统计法]({{ site.baseurl }}/image/excel17.png)

得到大类别的统计表，

![时间统计法]({{ site.baseurl }}/image/excel18.png)

同样排序，然后增加百分比选项，果然生活中的吃喝拉撒占去一半时间……

![时间统计法]({{ site.baseurl }}/image/excel19.png)

以上是看某一周的数据，如果想比较一下这周跟上周的差别，只需要将”week”从”filter”拖到旁边的”column"里面

![时间统计法]({{ site.baseurl }}/image/excel20.png)

然后最近五个星期的数据都出来了（因为我只有五个星期的数据），看起来上周的行政事务还不算多，之前两个星期的行政事务更多！擦！还有，开会的时间比做实验的时间多不少……所有的数据都一目了然

![时间统计法]({{ site.baseurl }}/image/excel21.png)

那么，我想看一下某一类别的细节，比如week 48的睡觉情况，只需要双击一下，就会自动跳出来一个新的表格，这一周我每天从几点睡到几点，不能够再详细了……

![时间统计法]({{ site.baseurl }}/image/excel22.png)

如果你是excel高手，你当然还可以得到更多更酷的统计，目前这些功能对我来说应该足够用了。而这一切，只需要几分钟就可以完成，相比柳比歇夫每次花费几个小时甚至几天去手动统计和总结，利用软件的效率无疑要高太多了。

2016-04-12

学会了写VBA，这样整个过程只需要1秒钟！[代码](https://www.evernote.com/l/Ap4Stt4TgGlAkp1H8bCOMaee235YTGUeepg)
