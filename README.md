

# Fribbels 第七史诗自动配装优化器

这是一款用于整理E7装备以及优化装备的工具。在这个游戏内一个角色的配装可能需要花费很多时间并且很难去组合一套最优的装备，所以我做了这样一个工具来使得配装过程更加容易一些。

请查看 [**快速入门**](https://github.com/Miztan/Fribbels-Epic-7-Optimizer#getting-started) 章节来学习如何使用这套工具。

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
  * [导入页](#importer-tab)
    + [从截图导入装备](#creating-a-new-gear-set-from-screenshots)
    + [从文件导入装备](#importing-a-gear-set-from-a-file)
    + [保存/载入装备及英雄](#save-load-gear-and-heroes)
    + [从Zarroc自动配装器导入装备](#import-gear-from-zarroc-optimizer)
  * [快速入门](#getting-started)
  * [结语](#closing-thoughts)
  * [疑难解答](#troubleshooting)
  * [联系我](#contact-me)

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


在这里你可以添加新的英雄或者管理现有的。我认为绝大多数按键都挺容易自己明白的，就其中一点需要注意的是 **添加额外属性** 页，这里可以让你为英雄添加神器/阵型属性，以进行优化配装。


![](https://i.imgur.com/tAytvsb.png)


SSS 克劳乌（宝马）用+30的亚乌利斯分摊神器，将会有 91 攻击 / 819 生命 / 以及 18% 的自阵生命。

## 导入页

![](https://i.imgur.com/LyJq3Lr.png)

该页面让你可以导入/导出不同的东西
_________________

### Creating gear data from screenshots

Select the folder you have your screenshots in and the app will start reading your screenshots. Make sure the folder only contains your screenshots and nothing else. This will then output your gear.txt file, and you can export it somewhere for the next step. If there are any errors reading the screenshots, the list of failed files will be shown.

### Importing gear data

Once you have the gear.txt file from the OCR step, choose the file and it will import the gear into the optimizer.

* *Append data* will add the new gears to your existing gears.
* *Overwrite data* will load in the new data, removing all previous items and heroes
* *Merge data* will combine your new gear screenshots with your currently loaded gear while keeping your heroes' equipped gear and builds intact.

If you want to wipe all your data and start clean with gear screenshots, use Overwrite.

If you have new screenshot files to add to a save, use the Append option.

If you already have a save, and you've screenshotted all your gear again, use Merge to replace old items with new items.


### Save/Load all optimizer data

Once you make changes to your items/heroes, the changes should be saved before you close the app. You can choose a file to save it to, and then later on load that file to import the data back in.

The app also does autosave to an 'autosave.json' upon changes being made, and will autoload whatever was saved to the autosave file the next time the app opens.


### Import gear from Zarroc optimizer

If were a user of Zarroc's gear optimizer, this lets you import your data directly from your existing Zarroc save file. All gear, heroes, and artifacts will be imported.


## Getting Started

Please read these instructions carefully!

**Installation:**

#### Windows

1. On the [Releases](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/releases) page, choose the latest release, and download the file that looks like ``FribbelsE7Optimizer-x.x.x-windows.zip``
    * Do not download the Source Code options, those won't work
2. Install **Java 8 - 64 bit** https://java.com/en/download/manual.jsp - Get the offline installer
    * After installing, restart your computer (required!)
3. Install an emulator to run Epic 7 on
    * I used LDPlayer, but others have worked as well: MeMu, Nox, etc. Bluestacks has issues with screen resolution, would recommend an alternative. See a solution for getting Bluestacks working [here](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/commit/94b8730e94e6323b278265ab46f6602ed7822c22#r45552268)
4. Set the emulator's screen resolution to **1600 x 900**. [Example](https://i.imgur.com/kyUQ86a.png)
5. Set Epic 7 to **English** and enable **High Quality Support** in settings. [Example](https://i.imgur.com/iEbfVN3.png)
6. Unzip the downloaded file, and run FribbelsE7Optimizer.exe (or FribbelsE7Optimizer.dmg/app on Mac) [Example](https://i.imgur.com/jltdg0U.png)

#### Mac OS/Bluestacks

1. On the [Releases](https://github.com/fribbels/Fribbels-Epic-7-Optimizer/releases) page, choose the latest release, and download the file that looks like ``FribbelsE7Optimizer-x.x.x-mac.dmg``
    * There is a dmg file and a zip file. Try the dmg first and if it doesn't work, try the zip. Mac version is still experimental.
    * Do not download the Source Code options, those won't work
2. Install **Java 8 - 64 bit**
    * Mac needs both JRE and JDK:
    * JRE: https://java.com/en/download/manual.jsp - Get the offline installer
    * JDK: https://www.oracle.com/java/technologies/javase-downloads.html
    * After installing, restart your computer (required!)
3. Install [Bluestacks](https://www.bluestacks.com/download.html)
    * Set the emulator's screen resolution to **1600x900** in the Preference menu
4. Configure keyboard shortcut for Screenshot
    * On your Mac: System Preference > Keyboard > Shortcuts Tab
      * Left Sidebar: Select App Shortcuts
      * Click the [+] button to add a shortcut
      * Application: Bluestacks
      * Menu Title: `Take screenshot` (any typo here will make it not work)
      * Keyboard Shortcut: Anything you want it to be
5. Back to Bluestacks: Install E7 from the Play Store and launch the game
   * Set Epic 7 to **English** and enable **High Quality Support** in settings. [Example](https://i.imgur.com/iEbfVN3.png)
6. Make sure to enter Full Screen Mode (Cmd+Shift+F) before starting your gear capture

**Importing gear screenshots:**

1. Open the Gear Management screen in Epic 7 and sort by Max Enhance<br><br>
2. Click each of the gears that you want to import, and screenshot it with your emulator's hotkey. Every screenshot should be **1600x900** and look **EXACTLY** like this: https://i.imgur.com/68A8Uf0.jpg

![https://i.imgur.com/ny7uaa8.jpg](https://i.imgur.com/ny7uaa8.jpg)

* Most emulators have a screenshot hotkey to make this easier: Ctrl + 0 for LDPlayer
* I would recommend screenshotting 10-20 gears to start with, then testing the rest of the steps to make sure the screenshots work before doing them all. I usually only screenshot the +9 to +15 gears for the optimizer.
3. Create an empty folder and collect all your screenshots into that folder.<br><br>
4. Go to the Importer tab, click on "Choose folder" under *Creating gear data from screenshots*, find your screenshots folder, and click Open Folder.<br><br>
5. The app will start reading the screenshots and your progress will be displayed. Once it is done, click Export, and save the *gear.txt* file.<br><br>
6. Under the *Importing gear data* section, click on Append data, and select your *gear.txt* file.<br><br>
7. Now you should see your imported gears under the Gears tab.

**Optimizing a unit:**

1. Add a unit on the Heroes tab, by selecting their name and clicking Add New Hero.
2. Select the new hero and click Add Bonus Stats. Here add any stats from your artifact, imprint, or EE. [Example](https://i.imgur.com/2aC22mN.png)
3. Go to the Optimizer tab, then select the hero. Fill in the main stats and set that you want into the right panel. [Example](https://i.imgur.com/3yfbkrE.png)
4. Fill in any filters you would like to apply. Each filter is described in detail in this section: https://github.com/fribbels/Fribbels-Epic-7-Optimizer#optimizer-tab
5. Hit Submit, and after processing a bit you should see a table of results.
6. Navigate the results with your arrow keys or mouse, select the result you want, and click Equip Selected.
7. You should now see your hero using those gears.
8. If you want to manually equip a certain item on a unit, go to the Gear tab -> Edit Selected Item -> Equipped. [Example](https://i.imgur.com/Bqs3ETL.png)

Here's a video that covers most of the importing process: https://www.youtube.com/watch?v=i_QW4INcZIE


**Updating the optimizer with new gear:**

* It helps to update the optimizer as you enhance/reforge gear. Add new pieces manually on the Gear screen or click the reforge icon to update 85 -> 90 gear.
* To import a bunch of new gear at once, screenshot only the new gear, then use the screenshot tool to generate another gear.txt file. Then use the *Append* option to add the gear.txt to your existing save file.
* If you want to re-screenshot all your gear, you can use the screenshot tool to generate the gear.txt again, and then either *Overwrite* your data to erase previous gear + heroes, or *Merge* the new gear.txt to replace old items and keep heroes/builds.

**Tips to get good optimization results:**

Here's some quick tips on getting the best results. This is assuming you've read the [Optimization panel](https://github.com/fribbels/Fribbels-Epic-7-Optimizer#optimizer-tab) descriptions.

* **Input the sets and main stats whenever possible.** This is the easiest way to narrow down results.
* **Use the substat priority filter and make sure to set your stat priority correctly!**
  * DPS units should have high priority on Atk / Cr / Cd / Speed for example.
  * Tank units should have high priority on Hp / Def / Speed for example.
  * Bad priorities will lead to bad results because good options get filtered out.
* **Lower the Top % to make the search faster, or increase Top % to search more results.** Most of the time I use 25-40%, sometimes lower if I want only my best gear on the unit.
* If you want a certain piece of gear to stay on a hero, go to the Gear tab -> Edit Selected Item -> Equipped and equip it on them first. [Example](https://i.imgur.com/oNO9ivL.png) Then you can use the optimizer with "Keep current" checked to keep that piece on them.

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

## Troubleshooting

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
