## Tasks on 2024/09/26

- 修改监控脚本
- 开始新的需求

### Summary

今天主要还是解决昨天的Reply机制的问题，Jax借助AOLink和源码帮我解决了这个问题。  

同时nvm多node版本安装不同AOS，我还没有实践。

目前来看流程我可以跑通了，oracle、server、processes。

理解跟上之后的话，从学习驱动，变为任务驱动开始专注代码之间的设计和风险。


### New Requirement
由Creat-Dataset调用Pool的Join-Pool, 并和前端联调

### Issues
今天遇到了一个Data类型不为字符串，reply消息无法发送的情况(也就是上面提到的问题)。需要新开一个分支提交PR，尽量将process中的tag和Data转化为字符串，以免阻碍正常交互。

之后交由Jax判断会不会影响与前端的交互。

### Gains
- AOLink辅助调试
- 由Reply机制引出的 对message交互流程的理解
- 通过修改PR 对项目的了解也有一定的增进