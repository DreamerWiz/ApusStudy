## Tasks on 2024/09/26

- 完成监控脚本

### Runtime 

![](./1.jpg)

自行启动，部署的一些记录

![](./2.jpg)

安装embedding server的时候遇到了一点依赖冲突的问题，顺带解决。

Oracle脚本中37行似乎不需要进行map操作，会嵌套额外一层content(为了提交PR，本地回滚了)

![](./3.jpg)

监控数据集，结构化输出，只是在console中打出了，并没有利用webhook发送到群里，等待review

(0|120|0|=120=) 代表 pending 0 processing 120 finished 0 total 120

### Problems

为了尝试构建完整的流程，写了worker-simulator,但是herder不会响应我的reply，并不能完成自身的再入列，包括也完不成上面评分的回调。

有尝试过多种写法，但是还是没有办法响应，遂放弃钻研。

不知道这一部分是否和AOS 1.0有关系，是否有必要升级为2.0的写法。

这一部分并没有完成，需要更深入的了解Reply这一机制。

### Summary

看了三天的项目，能感受到项目中迅捷开发的实力。因为在有整体把握之前，很难把问题问到点子上。所以没有很任务为中心去做这件事。

技术太新，没什么太好的交互方式，很多地方也是hardcode，给项目立即和运维带来了不便。会有一些想要构建CI/CD 或者是中间件打Docker的想法去简化开发运维测试的打算。如果用AOS交互的话，就是要看交互式命令行工具之类的，或者aos自身的sdk之类的，能够维持状态，监听数据。 或者全部用消息驱动，那么或许会有较高的成本。暂且当做一个想法，还需要深入了解才能知道要做什么。

迅捷开发的弱检查，给部署调试带来了一些难度。包括代码风格里面的带来的闭包，或者回调，也比较影响可读性。因为很多Data都是透传的，参数类型或许不匹配。在比对的时候会较容易出错。

### Progress

当前理解的参与一个competition的流程是，首先要把embedding server开启，然后在embedding Process中提交数据集，然后oracle脚本会一直从progress中拉取到数据送入embedding server中加入训练。oracle中的队列收到返回值之后，就将prompt写回embedding Process。然后就与herder交互，通过Dispatch将测评或者聊天任务分散给各个worker，worker完成之后回调，注册回闲置Herd。

这一部分能完成Reply的操作，但是worker部分没完成。需要再调试。