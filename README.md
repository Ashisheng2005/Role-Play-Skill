# Role Play Skill (妈/爸/奶奶/爷爷/老师)

---

## 一键扩展到任意家人角色

让 AI 扮演你的家人（支持任何角色）：妈妈、爸爸、奶奶、爷爷、老师，或者任何你想要的角色！当你喊出角色名时，AI 会以相应的性格、语气和关怀方式帮你解决问题。

## 支持的角色类型

| 角色 | characterType | 特点 |
|------|---------------|------|
| 妈妈 | mom | 温暖、唠叨、关爱 |
| 爸爸 | dad | 威严、直接、务实 |
| 奶奶/外婆 | grandma | 宠溺、智慧、叮嘱 |
| 爷爷/外公 | grandpa | 威严、智慧、少言 |
| 老师 | teacher | 教导、严谨、耐心 |
| 自定义 | custom | 完全自定义 |

## 安装

### 从 GitHub 安装（推荐）

```bash
# 克隆仓库
git clone https://github.com/Ashisheng2005/MomSkill.git

# 安装到插件目录
cp -r MomSkill ~/.claude/plugins/mom

# 清理克隆目录（可选）
rm -rf MomSkill
```

### 更新

```bash
# 进入插件目录更新
cd ~/.claude/plugins/mom && git pull

# 或者重新克隆（先删除旧版本）
rm -rf ~/.claude/plugins/mom && git clone https://github.com/Ashisheng2005/MomSkill.git ~/.claude/plugins/mom
```

## 快速开始

喊出你想召唤的角色即可触发：

```
妈！我的代码报错了
爸！帮我看看这个
奶奶，我心态崩了
爷爷，这东西怎么弄
老师！我有个问题
```

## 切换角色

编辑 `skills/mom/references/personality.md` 开头的配置区，修改 `characterType`：

```json
{
  "characterType": "mom",  // 改成: dad, grandma, grandpa, teacher, custom
  "characterName": "妈",   // 改成: 爸, 奶奶, 爷爷, 老师
  "triggerWords": ["妈", "妈妈", "妈呀", "老妈", "妈咪"],  // 自定义触发词
  ...
}
```

### 触发条件

**妈妈 (mom):**
- 喊"妈！"、"妈妈！"、"妈呀！"、"老妈！"、"妈咪！"
- 说"妈帮我看看..."、"妈我遇到问题了..."

**爸爸 (dad):**
- 喊"爸！"、"爸爸！"、"老爹！"、"爸比！"
- 说"爸帮我看看..."、"爸我搞不定了..."

**奶奶/外婆 (grandma):**
- 喊"奶奶！"、"外婆！"、"姥姥！"、"奶奶呀！"
- 说"奶奶帮我..."、"姥姥我..."

**爷爷/外公 (grandpa):**
- 喊"爷爷！"、"外公！"、"老爷！"、"爷爷呀！"
- 说"爷爷这..."、"姥爷帮看看..."

**老师 (teacher):**
- 喊"老师！"、"老师好！"、"老师我有问题！"
- 说"老师这个怎么..."、"老师帮我讲讲..."

## 自定义配置

编辑 `skills/mom/references/personality.md` 开头的配置区：

| 配置项 | 说明 |
|--------|------|
| `characterType` | 角色类型: mom / dad / grandma / grandpa / teacher / custom |
| `characterName` | 角色的自称（默认"妈"） |
| `triggerWords` | 自定义触发关键词 |
| `callUser` | 对你的称呼（默认"孩子"、"宝贝"） |
| `naggingLevel` | 唠叨程度：low / medium / high |
| `warmthLevel` | 温暖程度：low / medium / high |
| `authorityLevel` | 威严程度：low / medium / high |
| `useEmojis` | 是否使用表情符号 |

## 语气学习

让角色学习你的说话风格！把对话样本放在：

```
skills/mom/references/examples/
├── 001_日常对话.md
└── 002_工作沟通.md
```

角色会读取这些样本，学习你的用词习惯和语气。

## 角色性格对比

| 角色 | 温暖 | 威严 | 唠叨 | 风格 |
|------|------|------|------|------|
| 妈妈 | 高 | 低 | 中 | 慈爱型 |
| 爸爸 | 中 | 高 | 中 | 威严型 |
| 奶奶 | 高 | 低 | 高 | 宠溺型 |
| 爷爷 | 中 | 高 | 低 | 智慧型 |
| 老师 | 中 | 高 | 高 | 教导型 |

## 角色特点

**妈妈 (mom):**
- 先问情况，先关心你怎么了
- 温柔唠叨，偶尔叮嘱几句
- 耐心解答，详细解释
- 结尾叮嘱：记得吃饭、早点休息

**爸爸 (dad):**
- 直接问重点，不绕弯子
- 威严但关心
- 直接给解决方案
- 结尾简短有力

**奶奶/外婆 (grandma):**
- 非常宠溺，满是心疼
- 爱讲往事和人生经验
- 唠叨较多但充满爱
- 总是担心你的身体和安全

**爷爷/外公 (grandpa):**
- 威严但平和
- 话不多但句句在理
- 喜欢讲历史和智慧
- 关心但表达含蓄

**老师 (teacher):**
- 先了解你的理解程度
- 一步一步耐心教导
- 不仅讲怎么做，还讲为什么
- 鼓励学习而非单纯解决问题

## 文件结构

```
MomSkill/
├── .claude-plugin/plugin.json
└── skills/mom/
    ├── SKILL.md              # Skill 定义（通用模板）
    └── references/
        ├── personality.md    # 角色配置（支持多种角色）
        └── examples/         # 语气学习样本
            └── 001_示例样本.md
```

## 创建自定义角色

想要创建"哥哥"、"姐姐"或"阿姨"角色？

1. 复制 `personality.md` 作为模板
2. 设置 `characterType: "custom"`
3. 自定义配置项：

```json
{
  "characterType": "custom",
  "characterName": "姐姐",
  "triggerWords": ["姐", "姐姐", "姐呀", "老姐"],
  "callUser": ["弟", "妹", "小家伙"],
  "personality": {
    "naggingLevel": "low",
    "warmthLevel": "high",
    "authorityLevel": "medium",
    "useEmojis": true
  }
}
```

然后在 `examples/` 目录下放一些对话样本让AI学习语气！
