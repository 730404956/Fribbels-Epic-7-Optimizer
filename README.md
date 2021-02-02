

# Fribbels 第七史诗自动配装优化器

这是一款用于整理E7装备以及优化装备的工具。在这个游戏内一个角色的配装可能需要花费很多时间并且很难去组合一套最优的装备，所以我做了这样一个工具来使得配装过程更加容易一些。

请查看 [**快速入门**](https://github.com/Miztan/Fribbels-Epic-7-Optimizer#快速入门) 章节来学习如何使用这套工具。

包含的功能有:
 - 内建的装备截图识别以用于导入装备
 - 配装优化器可以主属性/次属性/套装等进行过滤
 - 自动从EpicSevenDB更新新英雄的数据
 - 计算英雄的额外属性（阵型/神器/专属装备等）
 - 装备次属性有效性评分
 - 重铸属性预测及编辑
 - 颜色标记结果排序

目前看上去是这样的:

![](https://i.imgur.com/dr0Gh1l.png)

## 系统需求
- 64位 Windows 或 MacOS
- 安装64位Java 8 （如果未安装，请从https://java.com/en/download/manual.jsp 下载离线安装包并进行安装）
_________________

**目录**:
  * [系统需求](#系统需求)
  * [自动配装页](#自动配装页)
    + [设置面板](#设置面板)
    + [属性过滤器](#属性过滤器)
    + [评分过滤器](#评分过滤器)
    + [次属性优先级过滤器](#次属性优先级过滤器)
    + [主属性及套装过滤器](#主属性及套装过滤器)
    + [次属性强制过滤器](#次属性强制过滤器)
    + [自动配装结果](#自动配装结果)
  * [装备页](#装备页)
  * [英雄页](#英雄页)
  * [导入页](#导入页)
    + [从截图创建装备](#从截图创建装备)
    + [从文件导入装备](#从文件导入装备)
    + [保存/载入装备及英雄](#保存/载入装备及英雄)
    + [从Zarroc自动配装器导入装备](#从Zarroc自动配装器导入装备)
  * [快速入门](#快速入门)
  * [结语](#结语)
  * [疑难解答](#疑难解答)
  * [联系我](#联系我)

## 自动配装页

在这里我会介绍自动配装器的不同部分，以肉逼瑞儿Build为例。有很多页面带有装备过滤的选项，我将一一介绍。

_________________

### 设置面板

![](https://i.imgur.com/oOz9b55.png)

该页面获得了其他页面的参数以进行设置。

- **英雄**: 从下拉菜单中选择你想要进行配装的英雄
- **强制模式**: 选择在强制面板中想要强制的次属性的数量（查看强制面板以获得更多详细信息）
- **预测重铸**: 预测在配装搜索中+15的85装备的重铸属性。注意：次属性预测并非100%准确，所以请准备好微调属性
- **最少1件85装备**: 只搜索至少包含1件85装备的配装
- **锁定装备**: 当该选项选中时，锁定的装备将会强制用于配装结果中。当该选项不选中时，锁定的装备将被忽略
- **已装备的装备**: 当选中时，已装备的装备将会用于自动配装。当不选中时，已装备的装备将会被忽略，除非该装备是在你当前需要配装的角色身上
- **保持现有的装备**: 当选中时，进行配装英雄身上的装备将会强制保留在身上，自动配装将只计算未装备的栏位
- **开始配装**: 点击以开始自动配装请求
- **过滤器**: 当自动配装完成时，点击按键将会以过滤面板内的属性将结果进行过滤
- **取消配装**: 中断并取消进行中的自动配装请求
- **载入设置**: 载入上一次对该英雄的自动配装设置
- **重置设置**: 将所有自动配装设置设定为默认值

_________________

### 属性过滤器

![](https://i.imgur.com/tVgubaV.png)

该面板将你自动配装结果以你规定的英雄属性以进行过滤。左边文本框代表最小值（包含），右边文本框代表最大值（包含）。如上面所说的瑞儿为例子，我们将会寻找一个瑞儿配装拥有如下属性：
- 最少2万血
- 最少2400防御
- 速度介于180~200之间


该过滤器仅会在你点击提交后才会将你的自动配装结果进行过滤。当过滤结果生成后，你可以制定一个更加严格的数值，然后点击 **过滤** 按钮。这将缩小你的配装范围，以避免重新进行一次配装计算。

_________________

### 评分过滤器

![](https://i.imgur.com/xmhk8ml.png)


该页面跟主属性页面有点类似，但适用于已计算好的属性。该评分并不会在游戏里看到，但这个可以帮助你决定哪一个配装更好。

- **HpS** -- `生命 * 速度` 评分. 对于单纯需要速度与血量而不需要其他属性的英雄来说，该评分非常有用。
- **Ehp** -- 有效生命, 计算公式: `血量 * (防御/300 + 1)`. EHP是一个用于衡量你英雄死亡前能承受的伤害量，该评分对于需要坦度的英雄来说非常有用。
- **EhpS** -- `有效生命 * 速度` 评分. 对于需要坦度与速度兼得的英雄来说，这个评分就很有用了。
- **Dmg** --  平均伤害, 计算公式: `攻击 * 暴击率 * 暴击伤害`. 用于计算你英雄的平均伤害。请注意，该评分将暴击率也计算在内，所以降低你的暴击率将会影响你的伤害平分，因为你暴击越少，就会拖低你的平均输出。
- **DmgS** -- DPS评分, 计算公式: `攻击 * 暴击率 * 暴击伤害 * 速度`. 该评分衡量了你的英雄能多快地打出伤害
- **Mcd** -- 最大暴击伤害, 计算公式: `攻击 * 暴击伤害`. 相对于Dmg平均伤害，该评分不考虑暴击率，并且假设你的英雄是100%暴击率，该评分对于只需要50%暴击率的英雄，或是PVE中攻击克制属性只需要85%暴击率时非常有用。
- **McdS** -- 最大DPS评分, 计算公式: `攻击 * 暴击伤害 * 速度`. 类似DmgS,只是不计入暴击率带来的影响。
- **CP** -- 这是你在游戏内英雄属性页看到的战斗力数值，但这并不考虑技能提升带来的影响。对于你想要用吃灰装备装在板凳角色用于世界BOSS来说非常有用。

在这个例子里，我们会优化寻找一个起码拥有20万的有效血量的瑞儿。
_________________

### 次属性优先级过滤器

![](https://i.imgur.com/i60uzCg.png)

**这个可能是最有用的过滤器，但使用前请务必先阅读好使用指南。用错了可能会将最佳配装排除在外**。

对每个次属性类型赋予优先级，从-1到3. 该优先级将会遍历每一件装备，并计算每个装备每一个次属性的属性值。属性值将会乘以你对每个次属性的优先级。然后将每一件装备的属性分加起来，并从最高的次属性分数进行排序。

 在这个例子中，我们主要是寻找一个又快又肉的瑞儿，所以我们指定如下的属性优先级:
- 血量与防御，高评分3，因为他们是最高优先级的属性
- 速度评分就低一点点，2
- 并且抵抗评分为1，该属性其实是一个对于瑞儿有用的属性
- 我们并不关心攻击/暴击率/爆伤/命中，所以这些属性的权重是0

然后，我们将最高百分比的滑块调整到30%。这将计算你所有的武器，并将根据你之前所制定的优先级来计算分数，然后只考虑前30%分数的装备以进行优化配装。然后对头盔、护甲等进行相同的操作。最后优化配装器会根据前30%的装备进行排列组合。

**要让该过滤器正常使用，必须将“最高百分比”滑块设置为100%以外的值**, 否则你将只会使用前100%的装备，没有任何装备会被过滤。值得一提的是，这种评分是一种启发式的方式，如果你设置最高百分比太低，那它并不总是产生最优结果。我发现30~50%区间是比较好的选择，因为50%会过滤大部分不相关的装备（比如你需求坦装，就会过滤掉DPS装，反之亦然）。低于30%的话，该过滤器就会变得过于敏感，那你可能就不会获得充足的装备来产生最佳配装结果，所以可能会错过最佳的配装结果，因为一下好装备已经被过滤掉了。多尝试一下不同的最高百分比值吧！

举个例子，像暗二五这样的纯DPS角色，优先级过滤器可能就会像下面这样，因为你只需要输出属性:

![](https://i.imgur.com/sdIG6xQ.png)

或者像肉逼泥巴哥一样，当你想要混合坦度，输出，命中，但不需要抵抗时。你可以把抵抗设置为-1来降低拥有抵抗属性的装备的评分。

![](https://i.imgur.com/CF3KmxT.png)

选择一个好的优先级过滤器，可以让你的优化配装容易很多，因为你不用去考虑不相关或者没什么卵用的装备搭配。
_________________

### 主属性及套装过滤器

![](https://i.imgur.com/fYOaDPB.png)

这个非常简单，我们正在寻找一套:
- 有生命%或者防御%的项链
- 有生命%或防御%的戒指
- 有速度的鞋子
- 速度套
- 抵抗或者免疫套

如果我们想要配装的角色不是很关心套装（比如暗拳或者其他类似的角色），这里就可以让我们用散件搭配。在这里需要注意的是暗拳需要免疫套，除此以外如果不需要其他的套装，留白就可以了。

![](https://i.imgur.com/8HEsbvY.png)

_________________

### 次属性强制过滤器

![](https://i.imgur.com/R8XjYhk.png)

请注意在设定页面中，我们之前设置强制模式为“最起码2个属性”。这里我们有3个次属性想要强制设定，所以用强制模式，我们就可以优化那些起码含有如下2个次属性的装备:
- 最起码3速度
- 最起码1 HP %
- 最起码1 防御 %

举个例子:
- 一件装备有如下次属性: 4 速/ 8% 攻击/ 16% 生命/ 8% 抵抗 就会通过这个过滤器，因为他符合起码2个属性:生命百分比和速度
- 一件装备有如下次属性: 2 速 / 8% 攻击 / 16% 生命 / 8% 抵抗 就会被这个过滤器过滤掉，因为只有一个次属性符合这个过滤器的要求: 生命百分比。 那这件装备在自动配装时就不会被计算在内。

设置次属性强制优化器对于缩小自动配装搜索时的范围是非常有用的，而且可以减少排列组合所以可以计算得更快。请注意你设定的过滤器，因为过于激进的过滤器可能会将你包里的好装备排除在外。因为你可能有一件 2 速度 / 40% 血量 / 100 防御数值 / 200 生命数值 的装备，但这件装备仍然会被过滤器排除掉，因为只有生命百分比符合要求，即使这件装备是有用的。
_________________

### 自动配装结果

![](https://i.imgur.com/zF1xKlE.png)

在这里你可以看到所有自动配装的结果，根据属性排序，也可以装备/锁定结果。
- 最顶那一行是你现在装备的装备属性
- 每一行都会被颜色标记，基于你设定的每个属性最小/最大范围
- 你可以用底部的箭头来在不同页之间进行翻页
- 全选/取消全选 会更改每件装备上的小复选框，或者你可以单独点击每一个复选框
- 装备按钮选中的话就会将该装备装备到英雄身上（同时顶掉他身上已装备的装备）
- 锁定按钮选中就会将选中的装备标记为锁定，这就会影响后续拥有“锁定”标记的装备的优化配装。
- 点击铅笔/锤子图标就会允许你编辑/重铸装备属性

## 装备页

![](https://i.imgur.com/W6bHn4Y.png)

在这里你可以找到一个包含你所有装备的表格，也可以对他们进行排序/过滤。底部的图标可以根据装备栏位和套装进行过滤，X 可以清除所有的过滤器。
**分数** 列是一个类似WSS的评分（我创建的），区别在于我将数值属性页计算在内，而WSS评分就忽略他们。评分计算依据是:
    分数 = 攻击百分比
    + 防御百分比
    + 生命百分比
    + 效果命中
    + 效果抵抗
    + 速度 * (8/4)
    + 暴击伤害 * (8/7)
    + 暴击率 * (8/5)
    + 攻击数值 / 39 * 0.5
    + 防御数值 /31 * 0.5
    + 生命数值 / 174 * 0.5

这用来评估你这件装备有多好，由85装备的最大属性值来进行缩放（速度最高为4，而不是5）。我发现数值属性的平均属性并用来评估数值属性的评分，0.5的倍数乘是随意设置的，但他的平均数值一般不如百分比数值。

![](https://i.imgur.com/fwqjtkF.png)

在这个页面里，你可以编辑现有的装备，或者添加新的装备，并填写相关字段。

## 英雄页


![](https://i.imgur.com/FnMbGWO.png)


在这里你可以添加新的英雄或者管理现有的。我认为绝大多数按钮都挺容易自己搞明白的，就其中一点需要注意的是 **添加额外属性** 页，这里可以让你为英雄添加神器/阵型属性，以便进行优化配装。


![](https://i.imgur.com/tAytvsb.png)


SSS 克劳乌（宝马）用+30的亚乌利斯分摊神器，将会有 91 攻击 / 819 生命 / 以及 18% 的自阵生命。

## 导入页

![](https://i.imgur.com/LyJq3Lr.png)

该页面让你可以导入/导出不同的东西
_________________

### 从截图创建装备

选择你截图所在的文件夹，本应用将开始读取你的截图。 确保该文件夹仅包含E7的截图，而没有其他内容。 然后将输出一个gear.txt文件，你可以将其导出到下一步。 如果读取截图有任何错误，将显示失败文件列表。 

### 从文件导入装备

当你在OCR步骤中获得了gear.txt文件后，选择文件，它将把装备导入到优化配装器中。 

* *新添数据* 会将新装备添加到你现有的装备列表中
* *覆写数据* 会载入新的装备数据，并删除旧的英雄和装备
* *合并数据* 会将你新装备与当前加载的装备合并在一起，同时保持英雄已装备的装备 

如果你想清除你所有的旧有数据并重新用新的截图开始，使用覆盖。

如果你有新的截图文件要添加到装备列表中，请使用“附加”选项。 

如果您已有存档，并且再次截图了所有装备，请使用“合并”将旧装备替换为新装备。 


### 保存/载入装备及英雄

对装备/英雄进行更改后，应先保存更改，然后再关闭应用程序。 您可以选择一个文件保存到该文件，然后在重新打开应用时加载该文件后并导入数据。 

进行更改后，该应用程序还会自动保存到“ autosave.json”，并在下次打开该应用程序时自动将保存的内容自动加载到自动保存文件中。 


### 从Zarroc自动配装器导入装备

如果你是Zarroc装备优化器的用户，这使您可以直接从现有Zarroc保存文件中导入数据。 所有装备，英雄和神器都会被导入。 


## 快速入门

请务必仔细阅读这些说明！ 

**安装:**

#### Windows

1. 在 [Releases](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/releases) 页面, 选择最新的发布版本, 然后下载一个类似 ``FribbelsE7Optimizer-x.x.x-windows.zip`` 名字的文件
    * 别下载源文件文件，那用不了的
2. 安装 **Java 8 - 64 位** https://java.com/en/download/manual.jsp - 下载离线安装包
    * 安装完后重启一下电脑 (必须!)
3. 安装一个安卓模拟器去运行E7
    * 我用雷电模拟器,但其他的模拟器应该也能用，比如Mumu，夜神等等。蓝叠因为在屏幕分辨率那里有问题，所以建议使用别的。如果你硬要使用蓝叠，那看看下面这个链接应该可以搞定 [蓝叠的解决方法](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/commit/94b8730e94e6323b278265ab46f6602ed7822c22#r45552268)
4. 将模拟器的分辨率设置为 **1600 x 900**. [Example](https://i.imgur.com/kyUQ86a.png)
5. 将E7设置为 **英语** 并在设置中开启 **高质量模式** . [Example](https://i.imgur.com/iEbfVN3.png)
6. 解压下载的文件，并运行FribbelsE7Optimizer.exe (或者在Mac上运行 FribbelsE7Optimizer.dmg/app ) [例子](https://i.imgur.com/jltdg0U.png)

#### Mac OS/蓝叠

1. 在 [Releases](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/releases) 页面, 选择最新的发布版本, 然后下载一个类似 ``FribbelsE7Optimizer-x.x.x-mac.dmg`` 名字的文件
    * 在那有个dmg文件和zip文件，先尝试下载dmg文件，如果dmg文件用不了再尝试zip格式，Mac版本还在测试阶段
    * 别下载源文件文件，那用不了的
2. 安装 **Java 8 - 64 位**
    * Mac需要同时安装JRE和JDK:
    * JRE: https://java.com/en/download/manual.jsp - 下载离线安装包
    * JDK: https://www.oracle.com/java/technologies/javase-downloads.html
    * 安装完后重启一下电脑 (必须!)
3. 安装 [蓝叠](https://www.bluestacks.com/download.html)
    * 在设置菜单里将模拟器的分辨率设置为 **1600 x 900**
4. 设置键盘截图快捷键
    * 在你的Mac的: 系统设置 > 键盘 > 快捷方式
      * 左侧边栏: 选择应用快捷方式
      * 点击[+]按钮去新增一个快捷方式
      * 应用:蓝叠
      * 标题: `Take screenshot`(必须英文)(这里打错了的话就用不了了)
      * 键盘快捷键: 这里你喜欢哪个就设哪个快捷键
5. 返回蓝叠:安装E7并打开游戏
   * 将E7设置为 **英语** 并在设置中开启 **高质量模式** . [Example](https://i.imgur.com/iEbfVN3.png)
6. 确保开始装备截图前，进入全屏模式 (Cmd+Shift+F)

**导入装备截图:**

1. 在E7里打开装备管理界面并选择按照'最大强化'排列<br><br>
2. 一一点击你想要导入的装备，并用你模拟器的快捷键进行截图，所有截图的分辨率必须为 **1600x900** 并且截图格式跟下图**完全一致**才能被正确识别: https://i.imgur.com/68A8Uf0.jpg

![https://i.imgur.com/ny7uaa8.jpg](https://i.imgur.com/ny7uaa8.jpg)

* 大部分模拟器都有截图快捷键的，比如雷电就是Ctrl+0
* 我建议先导入10~20件装备，测试一下余下的步骤确保这些截图正常导入。一般来说我只会截+9以上的装备导入到优化器里面。
3. 创建一个空的文件夹，并将你所有的截图保存在里面.<br><br>
4. 点击App里的导入页，然后在*从截图创建装备数据* 下面点击"选择文件夹"，选中你的截图文件夹并点击"打开文件夹".<br><br>
5. 然后App就会开始自动读取你的截图，并且会显示进度。当搞定以后就点击Export去将装备列表保存到*gear.txt*文件里.<br><br>
6. 在*导入装备数据*下面点击添加数据，并选中你上一步生成的*gear.txt*文件.<br><br>
7. 现在你应该就能在装备页里面看见你导入的装备了.

**为一个英雄优化配装:**

1. 在英雄页里面新增一个英雄，选好他们的名字然后点添加新英雄就可以了
2. 选择这个新英雄，并且给他们添加额外的属性。比如在这里你可以加点你这个英雄的自阵/神器属性/或者专属装备的属性. [Example](https://i.imgur.com/2aC22mN.png)
3. 进入优化配装页，然后选中你刚刚那个英雄，在右边面板填写你想要的主属性和其他选项（比如套装） [Example](https://i.imgur.com/3yfbkrE.png)
4. 填写那些你想要用上的过滤器，每个过滤器都已经在下面这个章节详细介绍过了: https://github.com/Miztan/Fribbels-Epic-7-Optimizer#自动配装页
5. 然后点击Submit按钮进行提交，过一阵子你应该就能看到结果列表
6. 选好你想要的装备组合，然后点击"Equip"按钮来装备上这套装备
7. 这你应该能看到你那个英雄穿上了这套装备了
8. 如果你想要手动一件件地装装备，去装备页->编辑选中装备->已装备. [Example](https://i.imgur.com/Bqs3ETL.png)

下面这有个视频涵盖了大部分的操作部分，可以看看学习下: https://www.youtube.com/watch?v=i_QW4INcZIE


**用新装备去更新优化配装器:**

* 当你强化/重铸装备时，它有助于更新配装优化器。 在装备页上手动添加新零件，或单击重铸图标以更新85-> 90装备。 
* 要一次导入一堆新装备，请仅对新装备进行截图，然后使用截图导入工具生成另一个gear.txt文件。 然后使用* Append * 选项将gear.txt添加到您现有的保存文件中。 
* 如果您想重新截图所有装备，则可以使用截图导入工具再次生成gear.txt，然后*覆盖*您的数据以清除以前的装备+英雄，或者*合并*新的gear.txt 替换旧装备并保留英雄/配装。 

**如何获得好的配装优化结果:**

以下是获得最佳优化结果的一些小Tips。 假设您已阅读[自动配装页]（https://github.com/Miztan/Fribbels-Epic-7-Optimizer#自动配装页）的说明。 

* **尽可能选择套装和主属性.** 这是最容易缩小配装范围的方法.
* **使用次属性优先级过滤器，并且确保你正确设定好这个属性优先级!**
  * 比如输出英雄应该对攻击/暴击/爆伤/速度有很高的优先级.
  * 比如肉逼单位应该对血量/防御/速度有很高的优先级.
  * 错误的优先级会导致很差的结果，因为好的选项都被你的过滤器过滤掉了.
* **降低最高百分比%来加快搜索速度，或者提高最高百分比%来搜索更多的结果组合.** 大部分时间我都用25~40%之间，有些时候会低一点，因为我只想我最好的装备装在这个角色身上
* 如果你想让某个装备留在英雄身上，请转至装备页->编辑装备->并先将装备在指定英雄身上。 [示例]（https://i.imgur.com/oNO9ivL.png） 然后，您可以使用已选中“Keep Current”状态的优化器，将其保留在该英雄身上。 

## TODO List

Hopefully this is useful for anyone looking for an easier way to gear their units.  There's still a lot of room to improve and I plan on adding new stuff as feedback comes in. I only work on this in my spare time, so please be patient with new features.

**Working on:**
 - v1.4.0
 - Dark mode

 **Medium priority:**
 - Cancel ongoing request when start is clicked again
 - Option to equip gear from heroes page
 - Move save/load to File menu
 - Use main stat gear for priority filter
 - Reapply all filters on Filter button press
 - Gear score column in optimizer results
 - Sum of substat priority column
 - Reforge non +15
 - When switching gears, popup asking to unlock the gears being unequipped
 - Heroes page: average gear score for each unit
 - Date newly added gear
 - Copying rows to text
 - Popup gear card
 - Show conversion/reforge mats
 - Customizeable # of 85 gear to filter, 0 - 6 lv 85s in results

**Bugs**
 - Comparison method violates its general contract

 **Low priority:**
 - Check if any gear is an upgrade to a unit
 - Update permutations on 4 piece set
 - Add can reforge, can enhance columns
 - Customize result limit
 - Clear out item previews on refresh
 - Optimize multiple heroes at once
 - Optimize results with a missing piece(s)
 - Add different level/awakening options
 - Tools for optimizing HP scaling units/skill scaling
 - Fix: See unit stats for whatever gear they have currently, not just for 6 pieces
 - Gear page, option to use more than one set/gear filter at time
 - Score per roll column in gear
 - Have two windows open at once
 - Select/interact with multiple heroes at once
 - Keyboard actions ctrl + a, ctrl + s, ctrl + arrows
 - Rage set damage calculation
 - Enable cross platform for Linux
 - Verify all imported screenshots are image files
 - Investigate decrypting network traffic for gear data

## 疑难解答

- If the optimizer doesn't work or doesn't load correctly:
  - Try restarting your computer, and reopen the app (there might be a child process still kicking around)
  - Try killing any java.exe processes in Task Manager that came from this app

 - If you're having problems with importing screenshot files:
   - Inspect your screenshots and make sure they are exactly **1600x900** resolution.
   - Make sure your Epic 7 settings have **English** and **High Quality Support** enabled.
   - Try moving your app and screenshot folder to a different location. (try the desktop)

  - If you're having trouble running the app after downloading:
    - If you don't see the .exe file, you might have downloaded the Source code instead of the binaries. Go to https://github.com/fribbels/Fribbels-Epic-7-Optimizer/releases and click on the 'FribbelsE7Optimizer-x.x.x...' file (for your specific OS)
    -   Error about a missing "ffmpeg.dll", you might have opened the file without unzipping it. Make sure to unzip/extract the .zip file after downloading it.

- If you see a "Error: EPERM: operation not permitted" error pop up while importing, there are a couple potential fixes:
  - Restart your computer, especially if you installed Java recently
  - Your antivirus might be blocking the app, try disabling it. I've seen issues with Avast specifically, and disabling Avast temporarily solves it.
  - Your file or folder contents might be compressed, uncheck this box on the folder: https://i.imgur.com/kSzTqek.png
  - Run the app as administrator
  - Move the app and screenshots folder to a new file location

- If you get a error that contains "Current relative path is C:\Windows\system32..."
  - I don't actually know the cause of this one, but one way to fix it is copying the data/tessdata/eng.traineddata/eng.traineddata file into the system32 path that its looking for

- If you're having trouble using it on Mac - "The application "FribbelsE7Optimizer" can't be opened":
  - Try unzipping the file using Unarchiver from the app store instead of Archive Utility. [Example](https://i.imgur.com/y9uGQcH.png)
  - Try downloading the .dmg file if you were using the zip/app file.
- If you're having trouble with Bluestacks/unable to resize the screenshots to 1600x900:
  - Windows: See possible Bluestacks workaround [here](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/commit/94b8730e94e6323b278265ab46f6602ed7822c22#r45552268).
  - Mac: Resize to 1600x900 through Bluestacks options, then restart Bluestacks, then click the green button to fullscreen Bluestacks. After its fullscreened, screenshots will come out as 1600x900.

- If a hero is missing from the drop down list, the data is being pulled from Epic7DB API so it may be an issue with that. If the hero is available in the Epic7DB API but not in this app, then contact me.
- If you see a bunch of optimization result rows with the same stats, you probably have duplicate gear. [Example](https://i.imgur.com/hUcyN1I.png)
  - Use the Duplicates filter on the Gear screen to find and fix your duplicate gear. Alternatively Overwrite/Merge your gear data to start over. Be careful when using the Append option, because that can result in duplicate gear being added.

## Contact me

Feel free to contact me on discord at fribbels#7526 for questions or comments or ideas/suggestions. If you ran into any issues, please check the [troubleshooting](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/#troubleshooting) section above first.

If you want to show support for the optimizer, you can [buy me a coffee](https://www.buymeacoffee.com/fribbels) or come say hi on discord!
