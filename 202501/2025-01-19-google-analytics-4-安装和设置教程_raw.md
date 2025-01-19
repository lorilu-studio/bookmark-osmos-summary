Title: Google Analytics 4 安装和设置教程

URL Source: https://xn--5hq58jg23b.com/ga4%E5%AE%89%E8%A3%85%E5%92%8C%E5%9F%BA%E7%A1%80%E8%AE%BE%E7%BD%AE%E6%95%99%E7%A8%8B/

Published Time: 2022-12-17T06:34:58+00:00

Markdown Content:
今天介绍的这款工具大家应该早就有所耳闻了——大名鼎鼎的Google Analytics——全球最流行的网站流量分析工具。作为一名独立站运营，连它都不熟悉的话怕是在这行混不下去的。这篇文章我将带大家使用GTM安装GA4代码并完成4项重要的基本设置。

什么是Google Analytics？
--------------------

Google Analytics（简称GA）是谷歌推出的一款用于数据收集、加工、分析工具。我们需要在网站上插入GA代码才能使它工作。

GA现在专指GA4，并且咱们也只能部署GA4。大家可能之前听过Universal Analytics（简称UA）这个名词，只不过UA已在2023年7月1日被官宣停止服务，所以我们现在已经完全没必要再学UA相关的内容。我网站的GA相关教程都指的是GA4。

另外，GA4有免费版和收费版之分，一般我们用的是免费版，大型企业才会用到收费版的GA360。

使用Google Analytics的好处？
----------------------

GA能帮我们收集访客在我们网站上的访问路径、转化记录、转化金额、访客来源国家等；我们可以通过查看GA平台上预设的报表或者自定义报表来了解整个网站的各项数据，进而优化我们的运营策略。

GA4安装和基础设置详细教程
--------------

教程分为注册GA4、为网站添加GA4代码、检查代码是否正常工作、GA4基础设置几个部分。

### 注册GA4

**第一步：**进入GA4官网：[https://analytics.google.com/](https://analytics.google.com/)，点屏幕正中间的 `开始衡量` 开始注册。

![Image 100: 注册GA4](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/1.%E6%B3%A8%E5%86%8CGA4.png)

注册GA

**第二步：**账号名称填自己能够识别的名称，底下的选择框全部勾选，进入下一步。

![Image 101: 新建账号](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E6%96%B0%E5%BB%BA%E8%B4%A6%E5%8F%B7.png)

新建账号

**第三步：**媒体资源设置。务必将时区设置成与[网站时区](https://xn--5hq58jg23b.com/wordpress%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B/#%E7%AB%99%E7%82%B9%E5%9F%BA%E6%9C%AC%E8%AE%BE%E7%BD%AE)、谷歌广告时区一致！

大家可能不明白保持时区一致性的用意，我举个例子就清楚了。以B2C网站为例，网站上的时区设置的是太平洋时间（UTC-8），而GA时区设置为北京时间（UTC+8），两者相差16小时。假如北京时间的5月1日上午来了20笔订单，反映在GA上的时间是5月1日，但是在网站后台显示的订单日期却是4月30日。那到时候网站数据和GA数据便不一致，分析起来会有误差。要是再叠加其他分析工具，那就会更混乱。虽然工具本身统计也会存在一定偏差，但是我们一定要把人为因素导致的偏差降到最低。

当然，这里即使设置错了也不要着急，之后在`GA设置>媒体资源设置>媒体资源详细信息`里面可以进行更改的。

![Image 102: 时区设置](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E6%97%B6%E5%8C%BA%E8%AE%BE%E7%BD%AE.png)

时区设置

**第四步：**填写商家信息。

![Image 103: 选择商家信息](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E9%80%89%E6%8B%A9%E5%95%86%E5%AE%B6%E4%BF%A1%E6%81%AF.png)

选择商家信息

**第五步：**选择业务目标。

![Image 104: 选择业务目标](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E9%80%89%E6%8B%A9%E4%B8%9A%E5%8A%A1%E7%9B%AE%E6%A0%87.png)

选择业务目标

**第六步：**接下来选择数据收集的来源，此时选择`网站`。

![Image 105: 选择数据源](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E9%80%89%E6%8B%A9%E6%95%B0%E6%8D%AE%E6%BA%90.png)

选择数据源

**第七步：**在出来的设置数据流界面，填入我们的域名以及可识别的数据流名称（主要为了区别web网站、app等不同渠道）。增强型衡量功能设置全部保持默认即可。

![Image 106: 创建数据流](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/6.%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E6%B5%81.png)

创建数据流

创建后将会出现数据流列表，点击刚创建的那条进入网站数据流详情的界面，我们之后会用到衡量ID。

![Image 107: 完成后的界面](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/7.%E5%AE%8C%E6%88%90%E5%90%8E%E7%9A%84%E7%95%8C%E9%9D%A2.png)

完成后的界面

这个页面先别关，后面在进行基础设置时还要继续在这个界面操作。

好了，到此GA4就注册好了，接下来就是为网站添加GA4代码。

### 为网站添加GA代码

在[GTM教程文章](https://xn--5hq58jg23b.com/google-tag-manager%E5%AE%89%E8%A3%85%E9%83%A8%E7%BD%B2%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B/)中，我已经在网站上完成了GTM代码的部署，接下来就要将GA4代码添加到GTM当中。

**第一步：**在GTM中点击新建代码。

![Image 108: 在GTM中新建代码](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/8.%E5%9C%A8GTM%E4%B8%AD%E6%96%B0%E5%BB%BA%E4%BB%A3%E7%A0%81.png)

在GTM中新建代码

**第二步：**在弹出界面将标题改为自己可识别的名称并对`代码配置`和`触发条件`进行配置。

首先配置`代码配置`。点击中间的图标，在右侧弹出框中选择第4项——`Google 代码`。

![Image 109: 选择Google代码](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/%E9%80%89%E6%8B%A9Google%E4%BB%A3%E7%A0%81.jpg)

选择Google代码

将上面GA网站数据流详情界面的衡量ID填入对应的文本框内。

![Image 110: 填入衡量ID](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/%E5%A1%AB%E5%85%A5%E8%A1%A1%E9%87%8FID.jpg)

填入衡量ID

设置`触发条件`。点击触发条件下的图标，在右侧弹出框中选择第3项——`Initialization - All Pages`。作用是当访客访问网站每个页面时都将触发GA追踪代码，记录相应的访问内容。关于界面中的3个触发器的解释说明详见[这里](https://support.google.com/tagmanager/answer/7679319?hl=zh-Hans&sjid=1023428467529107296-NC)，通俗的解释在我的GTM教程中有写。

![Image 111: 选择触发条件](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/%E9%80%89%E6%8B%A9%E8%A7%A6%E5%8F%91%E6%9D%A1%E4%BB%B6.jpg)

选择触发条件

点击右上方保存。

![Image 112: GA部署](https://xn--5hq58jg23b.com/wp-content/uploads/2024/07/GA%E9%83%A8%E7%BD%B2.jpg)

GA部署

**第三步：**GTM界面点击右上角 `提交` 按钮，正式完成GA代码部署。

![Image 113: 激活GA代码](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/13.%E6%BF%80%E6%B4%BBGA4%E4%BB%A3%E7%A0%81.png)

激活GA4代码

一般过24-48小时就能在谷歌分析中看到数据记录。当然，我们不妨先对GA代码是否可以正常工作进行检查。

### 检查GA代码是否正常工作

**方法一：**

回到GA的首页，同时在浏览器中打开我们的网站，过一两分钟再查看GA4首页右侧的过去30分钟用户数展示区中有没有记录。有记录就代表GA正常工作。

![Image 114: 通过GA实时访问视图查看](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/14.%E9%80%9A%E8%BF%87GA4%E5%AE%9E%E6%97%B6%E8%AE%BF%E9%97%AE%E8%A7%86%E5%9B%BE%E6%9F%A5%E7%9C%8B.png)

通过GA实时访问视图查看

**方法二：**

在GTM网站，点击右上角的 `预览` 按钮。

![Image 115: GA代码](https://xn--5hq58jg23b.com/wp-content/uploads/2024/07/GA4%E4%BB%A3%E7%A0%81.jpg)

GA代码

在跳出的 `Tag Assistant` 界面文本框内输入我们的网站网址，点击 `Connect` 。

![Image 116: 连接网站](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E8%BF%9E%E6%8E%A5%E7%BD%91%E7%AB%99.jpg)

连接网站

将会打开我们的网站，我们随便在上面点个链接就可以。然后回到tag assistant选项卡，可以看到页面中我们刚才新建的GA代码在`Tags Fired`下方，代表已被成功触发。证明GA是正常工作的。

![Image 117: GA代码已激活](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/GA%E4%BB%A3%E7%A0%81%E5%B7%B2%E6%BF%80%E6%B4%BB.jpg)

GA代码已激活

测试代码安装没有问题后，继续回到GA中完成一些基础但是重要的设置。

### GA4基础设置

以下各项设置均可在左下角齿轮界面找到。

![Image 118: GA设置](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/GA%E8%AE%BE%E7%BD%AE.jpg)

GA设置

#### 排除内部流量

使用GA的目的是获取数据并据此分析、得出结论，从而指导业务。所以数据的准确性是至关重要的。假如我们未进行设置，那么GA默认会记录所有访问者的访问数据，包括我们自己的各项访问行为。对于指导业务来说，我们自己或公司同事的访问数据完全没有任何价值，在频次高的情况下甚至会误导分析人员得出错误结论。那么后面运营人员按照错误结论瞎忙活半天，到头来却是没有半点作用。所以，我们必须要排除内部的流量。

回到刚才网站`数据流详情`界面，下拉到下方，点击  `谷歌代码 > 配置代码设置` ，下拉新的弹窗界面到设置菜单项，点击下方的 `展开` 按钮，就会出现`指定内部流量`的设置项。

![Image 119: 指定内部流量](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/%E6%8C%87%E5%AE%9A%E5%86%85%E9%83%A8%E6%B5%81%E9%87%8F.jpg)

指定内部流量

点击该设置项，出现新的弹窗，点击 `创建` 按钮，进到创建内部流量规则的弹窗页。

![Image 120: 设置内部IP](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/23.%E8%AE%BE%E7%BD%AE%E5%86%85%E9%83%A8IP.png)

设置内部IP

规则名称：填自己可识别的命名即可。比如公司、家里等等；  
traffic\_type 值：保持默认；  
IP 地址：将自己可能会经常用到的IP全添加进去。IP的匹配类型很多，根据实际选择。

Tips：  
1\. 只需百度输一下IP就能出现当前的IP地址；  
2\. 手机端在使用数据流量的情况下，ip地址是会变化的，故手机端无法很好地屏蔽掉，最好是使用wifi或者是固定ip的梯子访问网站；  
3\. 假如各位用的是非固定IP的机场，那IP也可能随时会变，也就没办法有效排除。

以下是我针对自用小鸡和家中WiFi的配置。点击右上方 `创建` 按钮完成规则创建。

![Image 121: 完成创建内部流量设置](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/24.%E5%AE%8C%E6%88%90%E5%88%9B%E5%BB%BA%E5%86%85%E9%83%A8%E6%B5%81%E9%87%8F%E8%AE%BE%E7%BD%AE.png)

完成创建内部流量设置

要使这条过滤规则生效，我们还需要`启用过滤`。

在数据过滤器界面，点击刚才创建好的排除内部IP的规则。

![Image 122: 数据过滤器](https://xn--5hq58jg23b.com/wp-content/uploads/2024/08/%E6%95%B0%E6%8D%AE%E8%BF%87%E6%BB%A4%E5%99%A8.jpg)

数据过滤器

下拉到底下的`过滤器状态`，选择 `有效` 并保存。这时过滤规则就正式生效了。

![Image 123: 设置为有效](https://xn--5hq58jg23b.com/wp-content/uploads/2024/08/%E8%AE%BE%E7%BD%AE%E4%B8%BA%E6%9C%89%E6%95%88.jpg)

设置为有效

另外，你可能还想排除机器人和蜘蛛产生的流量，其实[GA4已经自动帮我们排除了这些已识别的机器流量](https://support.google.com/analytics/answer/9888366?hl=zh-Hans)，不需要再额外设置。

#### 数据收集设置

对于我们来说，数据信息越丰富越好。根据[谷歌官方的说法](https://support.google.com/analytics/answer/9445345)，谷歌信号能在再营销、广告报告、“受众特征和兴趣”报告、跨设备报告等方面给我们带来更详细的数据。所以，我们最好在数据收集设置中开启谷歌信号。将这一页中能启用的都启用。

![Image 124: 数据收集](https://xn--5hq58jg23b.com/wp-content/uploads/2024/08/%E6%95%B0%E6%8D%AE%E6%94%B6%E9%9B%86.jpg)

数据收集

#### 数据保留时长设置

我们使用的GA4免费版默认只保留2个月的事件数据，这些的事件数据可能会影响我们在<探索\>报告栏目中的自定义数据报表的数据。所以，为了更好地分析较长时间维度的数据，毫无疑问我们需要将数据保留时长改为14个月。

![Image 125: 数据保留时长](https://xn--5hq58jg23b.com/wp-content/uploads/2024/08/%E6%95%B0%E6%8D%AE%E4%BF%9D%E7%95%99%E6%97%B6%E9%95%BF.jpg)

数据保留时长

提示：根据[谷歌文档](https://support.google.com/analytics/answer/7667196?hl=zh-Hans&utm_id=ad)的描述，事件数据过期是不影响标准报告的，只会影响探索报告。标准报告是谷歌提供的固定格式内容的数据报告。

![Image 126: 标准报告和探索报告](https://xn--5hq58jg23b.com/wp-content/uploads/2023/11/%E6%A0%87%E5%87%86%E6%8A%A5%E5%91%8A%E5%92%8C%E6%8E%A2%E7%B4%A2%E6%8A%A5%E5%91%8A.jpg)

标准报告和探索报告

当然，我们也可以保存更长时间的数据，这时就要用到Google的数仓——[Bigquery](https://cloud.google.com/bigquery)，用SQL语法查询。推荐有一定规模的公司使用。

#### 产品关联

我们还可以将GA和Google Ads、GMC、站长管理平台等关联起来，更充分地利用所有平台的数据。这样的话，各个平台的有关数据能够汇总到GA4的仪表盘内，方便数据的整合和透视。

![Image 127: 谷歌产品关联](https://xn--5hq58jg23b.com/wp-content/uploads/2024/08/%E8%B0%B7%E6%AD%8C%E4%BA%A7%E5%93%81%E5%85%B3%E8%81%94.jpg)

谷歌产品关联

多个站点的GA设置
---------

当我们有多个网站需要添加GA代码时，可以新建多个媒体资源或者多个账号，使用不同的衡量ID对不同网站进行独立追踪。千万别用同一个衡量ID追踪不同网站，否则数据会串！！！

![Image 128: 新增媒体资源](https://xn--5hq58jg23b.com/wp-content/uploads/2022/12/%E6%96%B0%E5%A2%9E%E5%AA%92%E4%BD%93%E8%B5%84%E6%BA%90.png)

新增媒体资源

总结
--

通过以上步骤，我们就完成了GA4的初始代码部署和一些基础但重要的设置。再经过一两天的数据收集，大家就能够亲自到GA界面查看到自己网站的各项指标了。当然，假如我们的网站是刚搭建的并没有其他流量，可能会没有数据，不用担心，等有访问了，自然会有数据生成。

另外，除了首页显示的实时访问数据以外，GA4的其他报表数据并非实时的，大约会延迟1-2天，耐心等待即可。
