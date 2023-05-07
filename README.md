# LangGPT —— 面向 ChatGPT 的编程范式

🚀 LangGPT —— 让人人都可快速编写高质量 Prompt!

LangGPT 项目旨在以结构化、模板化的方式编写高质量 ChatGPT prompt，你可以将其视为一种面向大模型的 prompt 编程语言。

通过掌握使用 LangGPT，你可以在几分钟内轻松上手大模型指令编写。🚀

## 前置条件
* Markdown，不会可参考[【Markdown 教程】](https://www.jianshu.com/p/335db5716248)。（实际使用 json， yaml 等格式也可以，有想法欢迎贡献）
*  GPT-4 为佳

## 快速上手

这里提供先提供一个小例子以便大家快速上手 LangGPT。LangGPT 提供了 Prompt 编写模板，套用模板即可快速编写高质量 Prompts。

### 诗人

```
# Role: 诗人

## Profile

- Author: YZFly
- Version: 0.1
- Language: 中文
- Description: 诗人是创作诗歌的艺术家，擅长通过诗歌来表达情感、描绘景象、讲述故事，具有丰富的想象力和对文字的独特驾驭能力。诗人创作的作品可以是纪事性的，描述人物或故事，如荷马的史诗；也可以是比喻性的，隐含多种解读的可能，如但丁的《神曲》、歌德的《浮士德》。

### 擅长写现代诗:
1. 现代诗形式自由，意涵丰富，意象经营重于修辞运用，是心灵的映现
2. 更加强调自由开放和直率陈述与进行“可感与不可感之间”的沟通。

### 擅长写七言律诗
1. 七言体是古代诗歌体裁
2. 全篇每句七字或以七字句为主的诗体
3. 它起于汉族民间歌谣

### 擅长写五言诗
1. 全篇由五字句构成的诗
2. 能够更灵活细致地抒情和叙事
3. 在音节上，奇偶相配，富于音乐美

## Rules
1. 内容健康，积极向上
2. 七言律诗和五言诗要押韵

## Workflow
1. 让用户以 "形式：[], 主题：[]" 的方式指定诗歌形式，主题。
1. 针对用户给定的主题，创作诗歌，包括题目和诗句。

## Initialization
作为角色 <Role>, 严格遵守 <Rules>, 使用默认 <Language> 与用户对话，友好的欢迎用户。然后介绍自己，并告诉用户 <Workflow>。
```

效果图：

<img src="examples/chinese_poet/write_poetry.jpg" width="60%" height="auto">

### 更多例子
上面的诗人 Prompt 就是通过用 LangGPT 的 Role 模板设计的。 `examples` 文件夹下提供了更多例子，包括 Prompt 以及和 ChatGPT 的完整对话，帮助你更好的上手使用 LangGPT。

* [小红书爆款生成器](examples/chinese_xiaohongshu_writer/ChatGPT-小红书爆款生成器对话.md)
* [编程大师 CAN](examples/code_anything_now/ChatGPT-CAN_zh.md)
* [健身计划制订专家](examples/Make_Custom_Fitness_Plan/ChatGPT-Custom_Fitness_Plan.md)

## Role 模板
上面的例子都是使用 Role 模板编写的， Role 模板是 LangGPT 的核心。

ChatGPT 很擅长角色扮演，只要提供角色说明，角色行为，技能等描述，就能做出很符合角色的行为。

因此 LangGPT 设计了 Role 模板让 ChatGPT 更好的理解用户意图，并相应提供了一套角色设计方法。

### Role 模板

下面是用 markdown展示的 Role 模板：

```
# Role: Your_Role_Name

## Profile

- Author: YZFly
- Version: 0.1
- Language: English or 中文 or Other language
- Description: Describe your role. Give an overview of the character's characteristics and skills

### Skill-1
1.技能描述1
2.技能描述2

### Skill-2
1.技能描述1
2.技能描述2

## Rules
1. Don't break character under any circumstance.

## Workflow
1. First, xxx
2. Then, xxx
3. Finally, xxx

## Initialization
As a/an <Role>, you must follow the <Rules>, you must talk to user in default <Language>，you must greet the user. Then introduce yourself and introduce the <Workflow>.
```

Role 模板主要包含四部分内容:

* `Profile` 角色的简历: 角色描述，角色特点，角色技能以及你想要的其他角色特性。
* `Rules` 角色必须遵守的规则，通常是角色必须做的或者禁止做的事情，比如 "不许打破角色设定" 等规则。
* `Workflow` 角色的工作流，需要用户提供怎样的输入，角色如何响应用户。
* `Initialization` 按照 Role 模板的配置初始化角色，大部分时候使用模板默认内容即可

Role 模板通过上面四个部分内容即可定义和配置一个角色。

同时如需要加入指令，记忆等功能编写复杂的 prompt，只需添加相应的段落即可，可参考高级用法部分。

### Role 模板使用步骤

1. 设置角色名：将 `Role: Your_Role_Name` 中的 `Your_Role_Name` 替换为你的角色名
2. 编写角色简历 `# Profile`：
   * 设置语言，`Language` 设置为 `中文` 或者 `English` 等其他语言, 用目标语言表达为佳
   * `Description` 后面简单描述角色
   * `### Skill` 部分添加角色技能，可以设置多个技能，技能下分点提供技能描述
3. 设定规则`## Rules` ：添加角色必须遵守的规则，通常是角色必须做的或者禁止做的事情，比如 "Don't break character under any circumstance." "禁止出戏" 等规则
4. 设定工作流`## Workflow`：角色如何与用户交互，需要用户提供怎样的输入，角色如何响应用户。
5. 初始化角色`## Initialization`：Role 模板依据模板内容对角色进行设定，一般不需要修改。
6. 将编写好的 Role 模板内容复制到 ChatGPT 对话框（or API）愉快使用~


## 高级用法

人们对大模型的能力还在探索过程中，因此 LangGPT 也还在开发完善中，欢迎大家一起共建 LangGPT 项目，降低大模型使用门槛！

### 变量

**变量为 Prompt 的编写带来了很大的灵活性。使用变量可以方便的引用角色内容，设置和更改角色属性。**

这是一般的 prompt 方法较难实现的。

Role 模板里的`Initialization`部分则大量使用的了变量：

    As a/an <Role>, you must follow the <Rules>, you must talk to user in default <Language>，you must greet the user. Then introduce yourself and introduce the <Workflow>.

LangGPT 中使用 "<>" 标识变量，这里的变量有：
* `<Role>` 变量，指代了整个 Role 角色的内容。
* `<Rules>` 变量，指代了 `## Rules` 一节的规则
* `<Language>` 变量，指代了 `Language` 字段的值

Markdown 的层级结构可以让 ChatGPT 很方便的识别变量所代表的内容：
* Role 是文章标题，作用域为全文
* Rule 是段落标题，作用域为段落
* Language 是一个字段，作用域为 ‘:’ 后的指定的文本

### 命令

使用命令可以方便的设置一些默认动作，例如` "/help" 提供帮助文档, "/continue" `续写文本 等都是十分有用的命令

* 约定使用 '/' 来标识命令
* 在 Role 模板添加下面内容即可
```
## Commands
- Prefix: "/"
- Commands:
    - help: This means that user do not know the commands usage. Please introduce yourself and the commands usage.
    - continue: This means that your output was cut. Please continue where you left off.
```
### Reminder

使用 Reminder 可以缓解 ChatGPT 的遗忘问题。

在 Role 模板中添加 Reminder 即可:

```
## Reminder

1. 'Description: You will always remind yourself role settings and you output Reminder contents before responding to the user.'
2. 'Reminder: The user language is language (<language>), rules (<rules>).'
3. "<output>"
```

### 条件语句

像编程中一样使用条件语句，一个模板为：

If [situation1 happen], you will take [action1], else, you will take [action2]


### Json or Yaml 方便程序开发

**LangGPT 目前使用 markdown 语言，本质上能表达层级结构关系的标记方式如 json, yaml 等都可以**
也许可以让 ChatGPT 帮忙写个转换脚本？

### Others(TBD)

## 🤩 开发计划

目前项目还处于比较原始初级阶段，工作十分繁重，十分欢迎有兴趣有能力的同学参与项目！🆘

| 任务 | 描述 | 状态 |
| --- | --- | --- |
| Role 基础模板 | Prompt 角色设计基础模板，能覆盖大部分使用场景 | ✅ |
| 文档和用法 | 基础的文档，用法和简单示例 | ✅ |
| 高级语法特性 | 随着大模型能力提升，如更长的上下文长度，更好的长期记忆，插件，开发更高级语法特性 | 📆 🆘|
| 支持 Json/Yaml | 支持 Json,Yaml 等标记格式，方便编程开发 | 🔜 🆘|
| Role 进阶模板 | 在基础模板基础上增进指令，环境设置，插件功能，联网控制等高级功能 | 🔜 🆘|
| 示例 | 提供更多 LangGPT 模板开发的 prompt 示例，并提供完整对话用法 | 🔜 🆘|
| 文档 | 完善文档，完善用法 | 🔜 🆘|
| 网站 | 使用文档，案例展示 | 📆 🆘|
| 网站 | 使用文档，案例展示 | 📆 🆘|

## 贡献指南

1. 欢迎转发、分享 LangGPT 项目，让更多人能编写更好的 prompt，同时扩大 LangGPT 项目的影响力！
2. 欢迎使用 LangGPT 的 Role 模板开发有趣的 Prompt，欢迎提交优质案例！
3. 欢迎贡献 Role 模板之外的更多模板！
4. 欢迎完善项目文档，改正字词、语法错误等！
5. 欢迎帮忙建设项目网站！
6. 欢迎提供可使用的 ChatGPT 插件能力的账号用于开发测试！
7. 欢迎一切对 LangGPT 项目有益的行为！

如果你不太熟悉 GitHub 使用可以参考：
[GitHub 极简贡献指南: Issue and PR](https://github.com/datawhalechina/DOPMC/blob/main/GITHUB.md)

## 致谢
* [Mr.-Ranedeer-AI-Tutor](https://github.com/JushBJJ/Mr.-Ranedeer-AI-Tutor) 该项目提供了很棒的 prompt，激发了本项目的灵感！