# e7
Epic7EquipmentEvaluateEmulatorExtraExtendedExtreme
# 快速上手
- 克隆本仓库（注意submodule的正确克隆）
- 更新数据
- 更新配装方案
- 运行v2.py
#依赖
- openpyxl
# 更新数据
## 标准数据
编辑Data/all.xslx文件，录入英雄、装备、神器
### 英雄
在【heor】表中编辑英雄的数据
填写【英雄】（A）、【等】（J）、【星】（K）、【觉】（L）列即可  
但由于Database的数据可能存在更新延迟等问题，也可以选择在详细面板数据（B~I）列填写数据，如果发现根据Database计算的数据与手动输入的数据不符，会采用手动数据并给出提示  
### 装备
在【weapon】、【head】、【armor】、【neck】、【ring】、【shoe】表中编辑装备的数据  
A列为套装，对应HP（生命）、AT（攻击）、DF（防御）、SP（速度）、HT（命中）、EV（抵抗）、CT（暴击）、CD（破灭）、FU（愤怒）、TO（夹击）、BL（吸血）、IM（免疫）、FB（反击）、PC（穿透）、WD（伤口）
B列为主属性类型，对应HPa（生命力）、HPp（生命力%）、ATa（攻击力）、ATp（攻击力%）、DFa（防御力）、DFp（防御力%）、SPa（速度）、HTa（效果命中）、EVa（效果抵抗）、CTa（暴击率）、CDa（暴击伤害）  
C列为主属性数值  
D至K列为副属性类型与副属性数据  
### 神器
在【artifact】表中编辑神器的数据  
【名称】（A）列为神器的名称  
【攻击力】（B）与【生命力】（C）为神器的增益  
【+】（D）列为神器的等级（此数据仅供更新时对比，对计算没有影响）
## 非标准数据
编辑new.json文件，录入数据库（Database）中未包含的英雄数据
# 更新配装方案
## 计算的方案
所有位于Plans目录下（不包括次级目录）的.xlsx文件都会被配装器导入进行计算  
在一个Excel文件中可以建多个表参与计算，每个表视为一份独立的方案  
【英雄】（A）列填入英雄的名称  
【第一条件】、【第二条件】、【第三条件】（B至D）列为计算方案  
E至I列为数值型阈值，可规定某一属性的上下限，默认为下限值，如果要同时规定上下限，采用分号（;）隔开，例如【209;218】，如果要仅规定上险，则在上限值前面加一个分号，即留空下限值，例如【;150】  
J至L列为套装型阈值，如果要指定某种套装，则在对应的列中填入1，否则留空  
【神器】（M）列填入配备的神器的名称  
【忽略愤怒】（N）列如果填入1，则不计算愤怒套的收益，对于假想对手不存在debuff的情况，建议填1  
【忽略穿透】（O）列如果填入1，则不计算穿透套的收益，对于AOE技能的英雄，建议填1  
【忽略暴击】（P）列如果填入1，则不计算暴击的收益，对于不暴击的英雄，建议填1  
AA至AK列为微调数据，可以根据具体阵容和英雄的情况对数据附加额外的加成，例如阵型加成、被动技能加成等  
# 计算
运行v2.py，等待计算完成
# 结果
计算完成后，在Result目录下会出现以方案文件的文件名命名的目录，其中会出现以方案的表名命名的.txt文件，计算结果记录在此文件中
# 贴士
## 方案的存档
可以将本次计算不需要采用的方案存在Plans目录的次级目录下（例如stack）  
这些方案都不会被加入此次计算  
在需要时则可以方便地拿出来
## 计算的继续
在执行计算时，如果对应的结果文件已经存在，那么对于结果文件中已经计算完成的英雄，会直接采用该结果
## 方案的微调
基于上述计算的可继续性，可以在已经计算的结果中删除某些英雄的内容，然后进行计算，实现部分英雄的更新
## 数据的管理
Excel表中的单元格样式可以自行操作，例如我将练满的装备都标黄，每次更新的时候就放心地跳过它们不需要检查，因为它们的数据不会再变化了；还有利用底纹区分不同职业的神器
# 引用
本项目引用了 https://github.com/kmalone86/gamedatabase 的数据库
