# **Surge 教程**

## Surge Tutorial｜Surge 小白教程




## 一、订阅导入

打开自己购买订阅的机场



**情况一**：自带一键导入Surge
![图片 1](https://github.com/dhjhb/Surge/assets/101947375/c7e4e0e2-c2ea-42bb-8085-7f2051f9887a)

**情况二**：无一键导入
![图片 2](https://github.com/dhjhb/Surge/assets/101947375/e6cf1125-d90b-473f-ad04-e737a174c6e5)
导入成功🏅

## 二、启动Surge

![图片 3](https://github.com/dhjhb/Surge/assets/101947375/6a43e3fe-8cfe-4ff7-93ee-ab556064bda3)

**备注**：允许Surge添加VPN配置时会跳转至设置要求输入锁屏密码，正常输入即可

再次点击启动键会提示证书未信任，下面进行证书安装并信任。
![图片 4](https://github.com/dhjhb/Surge/assets/101947375/5596c6d0-0130-4f82-a775-c7117c1c3fe9)

此时会跳转至浏览器
在浏览器中完成以下操作
![图片 5](https://github.com/dhjhb/Surge/assets/101947375/c00044dd-05ab-4659-9b60-880641f203e8)

完成上面两步操作后来到系统设置进行证书安装和信任
![图片 6](https://github.com/dhjhb/Surge/assets/101947375/27904e52-523d-4797-a17d-397d4c2bfb43)
点击关于本机->页面最下方证书信任->信任刚安装的证书
![图片 5 5](https://github.com/dhjhb/Surge/assets/101947375/bb770d9c-96ce-4027-a867-8d6a6148b4b6)


返回Surge可以看到证书系统已信任，可以正常使用了。

![图片 7](https://github.com/dhjhb/Surge/assets/101947375/cf5e4d63-58d0-4712-87fb-3de846b13e52)

**碎碎念**：出站模式的不同表示Surge对网络流量的接管程度不同。

  🚀直接连接表示Surge只进行简单的流量监看，不能实现“网络加速功能”。

  🌍全局代理模式下当前的所有流量将全部由Surge接管，通过当前选择的节点转发。

  🔀规则模式下的流量会按配置文件中的代理规则进行代理。一般机场的托管配置中设置的为可以国内直连的不通过代理，常见国外请求走预先选择的节点。（推荐使用，有省流、国内访问快等优点）

## 三、规则应用与策略组配置（规则模式）

**说明**：订阅机场给的众多节点并不是完全相同的，它们指向不同的国家，对不同网站或流媒体平台的支持效果也不同。一些机场的托管配置有对不同使用场景做适配，但个别时候还是需要自己去手动切换可用节点就十分麻烦。灵活运用Surge的策略功能便能方便的手动或自动切换节点。

**举个例子**🌰：当你要访问YouTube时，香港、台湾、新加坡的节点都可以访问，但如何将最快的可用节点指派给油管呢？这便要使用到规则与策略功能了。

![图片 8](https://github.com/dhjhb/Surge/assets/101947375/3dae4e88-7038-4361-a877-0002691e276b)
打开YouTube应用或网站后回到Surge，可以在工具的最近请求中找到明显来自YouTube的流量记录（明显带有“yt”、“google”、“gg”等流量记录也来自对油管的访问）。查看明细可以了解到我们的当前配置将带有“YouTube”关键词的访问流量被识别到并采用了分配给“香港｜HK03｜ND”这一具体节点的策略。


![图片 9](https://github.com/dhjhb/Surge/assets/101947375/c374d262-c0e4-46d6-accf-2497c8f25505)

这里可以对照[Surge使用手册](https://manual.nssurge.com/book/understanding-surge/cn/#转发代理和规则系统)来查看每一项的具体功能。下面是截取的部分。

![图片 10](https://github.com/dhjhb/Surge/assets/101947375/8a2b3147-52ff-4ec4-8942-76f7b894acc4)
配合不同规则类型的选择和简单的修改代理策略可以实现访问YouTube时走手动选择的固定节点。而要实现自动匹配某个国家的多个节点中最“合适”的，就要使用到策略组功能了。

![图片 11](https://github.com/dhjhb/Surge/assets/101947375/4a73acce-b8d2-4867-abed-cfaf15bcadf4)

在代理服务器中新增策略组，命名为YouTube，选择URL延迟自动测试（网速最快的节点、url-test）将下方可用的策略拖拽到包含的策略中后点击完成。

这时回到策略组会发现出现了名为YouTube的策略组。点击测速键会发现当前组启用的是延迟最低的节点（URL延迟自动测试的功能）

![图片 12](https://github.com/dhjhb/Surge/assets/101947375/3e51b18a-229b-48f8-abe0-81473fb97dbb)
利用这种方式我们可以将相同国家的节点放置在同一个策略组中，并使组内延迟最低的被调用。

![图片 13](https://github.com/dhjhb/Surge/assets/101947375/267ecddc-53dc-45c0-8d41-b4b1406eadc2)

此时距离实现我们的例子🌰就差最后一步了。将YouTube策略组中的代理策略替换成各个国家的策略组。这里可以长按YouTube策略组图标，编辑策略组，替换上国家策略组并将组类型改为select（手动选择）。

此时我们便达到了目的，但有几点问题还需解决。

1.一个策略组中添加大量节点时很不方便；

2.通过查看流量细节更改规则的方式很繁琐。

让我们先解决第一个问题。
那便是利用正则表达式进行关键词筛选（又提到了关键词呢）

我们这里以生成一个东亚的策略组为例。
在创建策略组时打开“包含所有代理策略”后会在最下方出现过滤器。通过半角“｜”间隔关键词可以将所有代理策略中含有所填关键词的节点筛选出来组成策略组。

![图片 14](https://github.com/dhjhb/Surge/assets/101947375/743e15c3-7348-4973-a8ce-49d99c656542)

同时我们可以将组类型为url-test的策略组隐藏起来，使得界面简洁。

（因为url-testl类型的策略组已经实现自动切换延迟最低节点，无需调整，可以隐藏）
那让我们带着第二个问题进行下一步骤吧

## 四、规则分流

**说明**：选择不同国家的代理节点访问相同的网站会有获得不同的内容和访问体验。

![图片 15](https://github.com/dhjhb/Surge/assets/101947375/68a2aca2-a837-4b46-b1d3-8e5b29a681c9)
例如用港澳台的节点访问bilibili可以观看大陆地区没有的内容。但这些内容的判定规则复杂，可能并不由单一的URL来决定。这就需要我们将来自bilibili的全部流量都指向一个国家策略组。


要想实现这个功能，解决第二个问题就迫在眉睫了。

这便要求我们掌握Surge中调用规则集的功能。

![图片 16](https://github.com/dhjhb/Surge/assets/101947375/603110e1-c10c-41a5-bd1a-66eecafe4680)

这里以添加GitHub的代理规则集为例。

先完成GitHub策略组的创建。

然后按照上图完成规则集的添加，这里的策略选择GitHub策略组。

在外部规则集填上

         https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/GitHub/GitHub.list

（也可以选择将链接文件下载后导入到Surge）

策略建议选择筛选所有节点中延迟最低的，以便于后续外部规则集使用时能更快与GitHub进行连接。

之后便可轻松访问[@blackmatrix7](https://github.com/blackmatrix7)大神的[规则仓库](https://github.com/blackmatrix7/ios_rule_script)来添加更多的规则集了。

我们继续以YouTube的规则集添加为例。
![图片 17](https://github.com/dhjhb/Surge/assets/101947375/4bf34ff2-4fd9-40c1-8777-7d7c81d4da46)

找到适配Surge端的一条YouTube规则集链接并复制。

回到Surge，按为GitHub添加规则集的方式给YouTube策略组添加规则集。
**因为访问YouTube时部分流量走在Google域名下，所以还需在YouTube策略组下添加Google的规则集或单独设置Google策略组并添加相应规则集。**

![图片 16](https://github.com/dhjhb/Surge/assets/101947375/603110e1-c10c-41a5-bd1a-66eecafe4680)

此时使用YouTube产生的所有流量都将通过导入的规则集进行关键词审查，审查确认的流量都将通过通过YouTube策略组进行流量代理。	


至此我们便可以通过重复以上步骤实现其他应用的规则分流配置。

**<u>！！！这里再次强调，如果导入的外部规则集较多，且更新间隔较短。建议为GitHub专门配置稳定较快的策略组，以保证在流量关键词识别过程中不断连。！！！</u>**

碎碎念：在我看来“网络长城”的基本工作原理是通过识别访问请求中的关键词来嗅探你的访问远端地址，被列入黑名单的远端地址被墙也就访问不了了。梯子的功能正是反其道而行之，提前识别到要访问的远端并与规则集这个“白名单”对照，记录在册的也就通过各种绕墙或穿墙方式避开“网络长城”的拦截了。

## 五、编辑配置文件（Mac端演示）

说明：想要高度定制化自己的代理配置，在手机上的小屏幕进行频繁的操作还是不太方便。好在Surge的配置文件允许我们自由编辑，为我们将配置文件提取->编辑->再次导入等一系列操作提供便捷。

前期准备：你需要一台电脑，可以编辑文本文件就行；或者你也可以将键鼠连接到手机上 。也不是不行；）
<img width="959" alt="截屏2024-03-28 16 36 40" src="https://github.com/dhjhb/Surge/assets/101947375/bfcac3c4-95bf-4340-957c-2794aa3e6d54">

言归正传让我们开始操作。

### 第一步：配置文件导出


按照下面的步骤将配置文件分享到电脑。如果没有电脑可以在文本模式中编辑，或导出到其他可行的软件中编辑。

![图片 5 1](https://github.com/dhjhb/Surge/assets/101947375/b3f20679-4ce7-427d-acb1-974bae2b1bdb)

我们便得到了一个后缀名为.conf的文件，用文本编辑打开它。*你可以在项目文件中找到这个演示文件，或许能用来作为模板使用*

<img width="555" alt="截屏2024-03-28 16 45 08" src="https://github.com/dhjhb/Surge/assets/101947375/ca29c218-39e2-4bb2-b447-94dc243688af">

### 第二部：对照更改

说明：在我们正式编写之前先让我们回忆下之前的操作。

我们完成了：

1. 机场订阅导入

2. 证书的安装与信任

3. 托管配置的副本创建

4. 策略组的创建

5. 策略组添加规则集

   

   这些操作中部分便可以在配置文件中找到对应内容。

   

   最前面的部分是我们的机场托管配置中的一些设置内容，副本的创建过程对这部分并没有影响。之前的操作我们没有修改，这里也不建议修改。
   
<img width="707" alt="截屏2024-03-28 20 40 24" src="https://github.com/dhjhb/Surge/assets/101947375/e8bebade-a51f-4979-ae1e-122401016d19">
接下来的部分便是机场的节点列表了，我们删除了其中关于机场订阅信息的内容。如果你在实际使用过程中不想保留那些信息，你也可以删除它们。

可在节点列表中添加🚀直接连接 = direct 方便后续策略组调用.

<img width="728" alt="截屏2024-03-28 20 41 27" src="https://github.com/dhjhb/Surge/assets/101947375/02c19fa9-07fc-4dc2-ad62-c6db3a29160e">

这便是可以删掉的节点，它们也称为*非法节点*

<img width="1514" alt="截屏2024-03-28 17 26 12" src="https://github.com/dhjhb/Surge/assets/101947375/ee7a6540-8c29-49c1-b7a8-4514b9be69ca">

我们导入节点后对节点进行了分类，将指向相同国家的节点放置在了同一个策略组中。

<img width="1034" alt="截屏2024-03-28 17 29 15" src="https://github.com/dhjhb/Surge/assets/101947375/ad625a57-7bb0-4b9f-bda2-08c3235af072">

我们对图中内容进行下详细说明。

一、以*香港*策略组为例，此节点采用URL- test类型，会将后方所有存在的所列节点进行延迟比较并调用延迟最低的节点。

二、对比我们设置的不同类型的策略组如*东亚*与*香港*，我们会发现它们在节点外还有些不同。你可以对照下表了解这些不同之处代表什么。

|                设置代码                |                             功能                             |                对应图形功能键(策略组设置界面)                |
| :------------------------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|           url-test/fallback            |                 控制对后方节点的选择调用方式                 | ![0A122A4C-FBF4-4C5E-969C-D5F3A566672F_1_201_a](https://github.com/dhjhb/Surge/assets/101947375/db9fe847-a4c1-47c7-81f9-4ba0d2c60281) |
|              no-alert=0/1              |              关闭策略变换通知/开启策略变换通知               | ![06C35D4E-9F6B-4D74-8781-B4AAD919069C_1_201_a](https://github.com/dhjhb/Surge/assets/101947375/7704881b-cde5-4b40-b4a0-d30ec17722a3) |
|               hidden=0/1               |                    隐藏策略组/显示策略组                     | ![062E7AED-7B7C-42CD-A4C2-CCE3C56AAFE8_1_201_a](https://github.com/dhjhb/Surge/assets/101947375/f33be0f2-7842-4abe-aabb-5702b56b17b5) |
|        include-all-proxies=1/0         |             包含所用代理策略/不包含所用代理策略              | ![2F78C34C-889E-45F7-BCDE-19F796279F8C_1_201_a](https://github.com/dhjhb/Surge/assets/101947375/c174fd4a-2186-403a-b26d-e73a7c67d0af) |
| policy-regex-filter=台\|新\|韩\|港\|日 | 开启包含所有代理策略时通过正则筛选节点<br />(以开启包含所有代理策略为前提)<br />(正则表达式中使用半角间隔号) | ![81086429-242E-4D24-9B6E-ABF505E2B776_1_201_a](https://github.com/dhjhb/Surge/assets/101947375/28d0aea2-249b-4789-b86a-531cf6c93970) |
|           update-interval=0            |                 更新间隔时间设置(不建议修改)                 |                        无对应图形窗口                        |

认识了这些代码元素的功能,我们便可以方便美观的完善国家策略组设置了.

利用正则表达式筛选节点建组十分方便,可以学习[@cdoco](https://github.com/cdoco)的[正则表达式](https://github.com/cdoco/learn-regex-zh)这篇文章来进一步了解.

对应用程序或网络域名设置策略组就相对简单很多.

<img width="1064" alt="截屏2024-03-28 20 55 49" src="https://github.com/dhjhb/Surge/assets/101947375/3b6d30ec-8f5b-4d7f-a27f-486325c543af">

以上我们同时新设置*Telegram*、*bilibili*两个策略组,并为它们安排了可选的几个国家策略组.

我们在Surge应用中已经完成了*GitHub*、*YouTube*、*Google*三个策略组的规则集设置.可以在下方看到设置的规则集链接.如下

    [Rule]
     #规则集-----------------------------
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/GitHub/GitHub.list,GitHub
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/YouTube/YouTube.list,YouTube
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Google/Google.list,Google
我们用为Telegram添加代理规则集来做一下操作对照.

按下图操作,在策略中选择Telegram后在外部规则集中添加[规则仓库](https://github.com/blackmatrix7/ios_rule_script)中的规则集链接后,会在配置文件规则部分([Rule])出现以下代码.    

    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Telegram/Telegram.list,Telegram

![图片 5 2](https://github.com/dhjhb/Surge/assets/101947375/f37347d5-0630-4b8c-9648-91997cdf34ec)

通过对照你便发现了这个步骤中Surge图形交互与代码内容的对应关系.以此可以直接编写bilibili的策略规则了.
          
    [Rule]
     #规则集-----------------------------
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/GitHub/GitHub.list,GitHub
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/YouTube/YouTube.list,YouTube
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Google/Google.list,Google
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/Telegram/Telegram.list,Telegram
    RULE-SET,https://raw.githubusercontent.com/blackmatrix7/ios_rule_script/master/rule/Surge/bilibili/bilibili.list,bilibili



第三部:导入修改后的配置文件
  
  确认你修改的配置文件内容正确后保存conf文件,发送到手机后用Surge打开便能直接导入使用了.

🎉🎉🎉🎉🎉🎉到现在你便学会了通过直接编辑配置文件的方式来配置代理.

后面更新通过Surge实现去广告的效果.
  














