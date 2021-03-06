# 高保真与组件开发checkList
## 开发前
1. **设计稿标注**：每个页面包含PC与移动端两份，检查需要标明宽高等样式的模块是不是标注清楚（UED方由于设计稿导出问题会出现某些大模块是图片，要注意），检查设计稿中的相关图标图片有没有给全。关于设计稿中未标明的相关效果（注入动画，悬浮效果等）需要UED给出另出一份文档说明，另外UED一般会发一份**原型图交互链接（标明了一些交互逻辑）**，这个可以一起要过来。

2. **需求说明文档**：主要是页面涉及到一些在设计稿中无法体现的页面功能，一般由产品经理提供，也就是详细的需求说明（目前很多需求在vision单上只有简单的两行背景），特别是涉及到组件开发，哪些地方需要配置成模板，文本部分是不是支持富文本，涉及到登陆注册等以用户信息为基础的都要给出比较详细的说明，有流程图最好。

3. **后台接口文档**：高保真涉及到后台接口，特别是外部接口前提是要清楚接口需要什么参数，返回的数据结构模型，能不能在本地开发模式调通，支持哪些域名下的请求，一般外部接口没有明确的诉求不会给一个详细的文档（直接甩接口说明地址，不一定看得懂），但是最终的目的是要把接口的细节弄清楚，接口是一件比较重要的事情，要提前确认好。

4. **需求分析会**：需求分析会是最终确立需求，评估工作量后正式进入开发的宣讲，主要是UED针对设计稿对交互的一次较为细致的讲解，最好拉上UED，测试人员，前端开发，PEP后台开发，外部接口开发和产品经理。人员具备后，后期的工作才不会出现测试，后台等开发一脸懵逼的情况。

5. **开发计划甘特图**：开发周期如果较长（超过1周），自己评估工作量后绘制一个开发计划甘特图，明确各个人员在特定时间需要做的事情，这个对于掌握开发自身的开发节奏有比较好的意义。如下图：

### 总结
关于开发前的准备，我们的期望是以上材料都能准备齐全，但是往往因为时间，相关人员配合程度，没有一个完整的文档材料，但是我们最终目的是确立开发的计划，一些小细节不太影响工作量的（注入几个图标缺失）可以暂时忽略，等之后给出，但是涉及到较为复杂的交互逻辑没有说清楚，只给个大致的想法，或者是接口人员都不确定的情况，一定要提出来让产品经理或者业务方及时沟通解决，不然开发进入中期再去要求，很大几率会发生返工的情况。

## 开发中
1. **时间安排**：对照开发计划甘特图的日期进行开发，已超过甘特图半天至一天的开发进度为宜（经常会有其它需求插入的情况）。

2. **需求变更**：需求变更的工作量超过2个小时需要产品经理或者业务方和主管沟通确认，增加工作安排时间。

3. ### **开发细节**：
#### 文字字体问题
设计稿中经常会出现roboto-medium,roboto-regular等浏览器不支持的字体说明，字体方面参照下表给出css样式，另外字体注意css资源中的默认body字体兼容值，和设计确认好。

#### 文字省略问题
文字的超出...，悬浮小框显示完整内容等等样式问题我们在其它css技巧文档中统一编排给出。

#### 头部banner
头部banner设计文字垂直居中，背景图拉伸和等比缩放问题。

#### 悬浮动画
很多标题文字有悬浮动画（变红，transition等等）。

#### 兼容适配
按楼层考虑PC和移动端的适配，这样会减少漏掉的适配问题。

关于开发细节会找时间写一份更详细的开发技巧文档。
## 开发后
开发后主要涉及的是页面上线后检视出现样式上的问题，或者产品经理提出某些需求变更，超过半小时开发量就需要另外排期修改了，因为涉及到发布，工作流，开发环境，任务切换等等问题，处理时间可能会超过1个小时，在手上有多个需求的同时一定要给自己留下较充足的开发时间，开发目前面临的现状很多是多个工作任务的切换，和各种产品经理，运营，开发，测试沟通，会议，经常有很多时间在无形中消耗掉了，需要时刻记得给自己一个弹性时间。

这是本次高保真+组件开发的一个初版的checklist和一些经验总结反思，后面随着需求的不断积累，文章会随时保持更新。