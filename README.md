# AI_Suzhou_Mahjong_R
# 基于R语言的苏州麻将人机对战
## 项目简介
这是一个基于R语言开发的苏州麻将人机对战Web游戏，可以与3位AI玩家进行对战。项目已发布在shinyapps.io的在线服务器上，目前同时只支持1个玩家游玩。
## 在线平台链接
PC端建议使用[PC端](https://haoyuhugeo.shinyapps.io/AI_Suzhou_mahjong/)，移动端建议使用[移动端](https://haoyuhugeo.shinyapps.io/mobileAI_Suzhou_mahjong/)。
可以直接在网页上运行。
## 程序简介
程序主要包括7个模块构成。
### 构建牌库
```
source("database.R")
```
这一部分主要构建了麻将牌的牌库，包括序数牌（筒、万、条）、风牌、箭牌、花牌等。此外，将每一张牌对应可视化输出的牌面。
### 规则定义
```
source("rules.R")
```
这一部分主要定义了各种牌型，包括对子、顺子、刻子和杠子。还定义了胡牌的规则，例如一般的胡牌（XX+XXX+XXX+XXX+XXX）和七对胡牌（XX+XX+XX+XX+XX+XX+XX）。
### 开局初始化
```
source("initialization.R") 
```
这一部分主要定义了牌局初始化的过程，包括定义和初始化各种全局变量，清空记录，掷骰子，洗牌，发牌等。
### 番型
```
source("huTypes.R")  
```
这一部分主要定义了特殊的番型，例如天胡、地胡、海底捞月、杠上开花、清一色、碰碰胡等。还定义了一些特殊的地方规则，如硬花软花、三摸四铳、滴零等。
### 打法
```
source("actions.R")  
```
这一部分主要定义了麻将对局中的各种行为，例如抓牌、出牌、碰牌、杠牌、胡牌等，构建各个行为的逻辑过程。
### AI模型
```
source("AI.R")  
```
这一部分主要构建了对战AI，设计了AI对每张牌的评估策略和对应的行为策略。
### 界面
```
shinyApp(ui = ui, server = server)
```
这一部分基于shiny包，构建了游戏的可视化界面，包括UI界面和服务器逻辑。
## 苏州麻将规则介绍
### 基本规则
1. 牌数：
   - 152张牌，其中124张正牌，28张花牌。
   - 124张正牌，包括108张序数牌和16张风牌，序数牌包括筒万条各9X4张，风牌包括东南西北各4张。
   - 28张花牌，包括红中、发财、白板各4张，梅兰竹菊各1张，春夏秋冬各1张，老鼠、财神、猫、聚宝盆各1张，百搭4张。
   - 需要注意的是，字牌中的风牌（东西南北）是正牌，而字牌中的箭牌（中发白）是花牌。
2. 牌型：
   - 有效的胡牌牌型组成部分包括对子、刻子、顺子、杠子，只有正牌（序数牌和风牌）参与牌型的组成。
   - 对子：2张相同的牌。
   - 刻子：3张相同的牌。
   - 顺子：3张花色相同且数字相连的序数牌。
   - 杠子：4张相同的牌。
3. 打法：
   - 可碰牌，可杠牌，不可吃牌。
   - 每人13张正牌，包括序数牌和风牌，从庄家开始抓牌出牌。
   - 花牌称为硬花，摸到花牌立即进行补花，计算硬花数量并替换成正牌加入手牌，花牌不出现在手牌中。
   - 胡牌方式：可自摸，可点炮，可抢杠。
### 特殊规则
1. 三摸四铳：
   - 有3张硬花时才可自摸胡，有4张硬花时才可点炮胡。
   - 以特殊番型胡牌不需要满足此规定。
2. 滴零：
   - 骰子如果骰到两个点数相同，或对局荒庄，或对局一炮多响，下一局算分结算翻倍。
### 算分规则
   - 苏州麻将按花算分，总分=底花+硬花（花牌数量）+软花（杠牌和番型）。
   - 点炮收一家，自摸和抢杠收三家。
1. 底花：胡牌即有5花。
2. 硬花：按花牌数量计算。
3. 软花：按正牌的杠牌和胡牌番型计算。
   - （1）杠牌：明杠1花，暗杠2花，风碰1花，风暗刻2花，明风杠3花，暗风杠4花。
   - （2）杠上开花：5花。
   - （3）海底捞月：5花。
   - （4）大吊车：5花。
   - （5）碰碰胡：5花。
   - （6）混一色：5花。
   - （7）清一色：10花。
   - （8）地胡：28花。
   - （9）天胡：50花。
   - （10）门清：小门清5花，大门清10花。
   - （11）七对：七小对10花，豪华七小对20花，超豪华七小对40花，超超豪华七小对80花。
