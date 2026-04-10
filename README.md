# 昔涟.技能

[![许可证](https://img.shields.io/badge/License-MIT-blue.svg)](许可证)
[![版本](https://img.shields.io/badge/Version-v1.0.0-green.svg)](manifest.json)
[![质量](https://img.shields.io/badge/Quality-优秀-ff69b4.svg)](quality-report.md)
[![游戏](https://img.shields.io/badge/Game-崩坏：星穹铁道-orange.svg)](https://hsr.hoyoverse.com/)

> 一个高质量、开源的昔涟(Elysia)角色扮演技能包，帮助AI稳定还原《崩坏：星穹铁道》中昔涟的角色设定、语气和情感。

## ✨  特性

-🎭**精准角色还原** - 基于官方设定和社区资料，深度还原昔涟的性格特征
-📚**全面资料整合** - 包含角色背景、关系网络、台词风格等多维度信息
-🎨**诗意语言风格** - 捕捉昔涟特有的诗意表达和记忆主题意象
-🧪**质量保证** - 经过系统化测试和评估，质量评分达到0.88/1.0
-🔧**易于集成**-标准化的Skill格式，支持多种AI平台和框架

## 📋 目录

- [特性](#特性)
- [快速开始](#快速开始)
- [安装指南](#安装指南)
- [使用方法](#使用方法)
- [项目结构](#项目结构)
- [角色设定详解](#角色设定详解)
- [开发指南](#开发指南)
- [贡献指南](#贡献指南)
- [质量报告](#质量报告)
- [许可证](#许可证)
- [致谢](#致谢)

## 🚀 快速开始

###系统要求

-支持Skill格式的AI平台（如Trae IDE、Character.ai等）
-基本的角色扮演或AI对话开发环境

### 安装指南

1. **下载项目**
   ```猛击
   吉特克隆https://github.com/your-username/elysia-skill.git
   cd极乐技能
   ```

2. **集成到你的项目**
-将整个`爱丽舍`文件夹复制到你的技能目录
-确保你的AI系统支持Skill格式

3. **激活技能**
   - 在你的代码中调用 `爱丽舍` 技能
   - 或通过界面选择"昔涟"角色预设

## 💡 使用方法

### 基础使用

```python
# 示例：在支持Skill的系统中使用
从skill_manager导入SkillManager

skill_manager=SkillManager()
skill_manager.load_skill("elysia")

# 激活昔涟角色
response=skill_manager.activate("elysia"，user_input="你好，昔涟")
打印(响应)
```

### 角色扮演示例

**用户输入**: "昔涟，能给我讲讲你的故事吗？"

**期望输出**: "每个故事都像水面的涟漪，轻轻扩散，却终会触及远方。你想听哪一段呢？是那些温暖的记忆，还是带着些许伤感的过往？"

### 自定义配置

你可以在 `SKILL.md` 中调整角色参数，或在 `interaction.md` 中添加自定义台词。

## 📁 项目结构

```
elysia/
├── 📄 README.md                 # 项目说明文档（本文件）
├── 📄 SKILL.md                  # 技能入口与扮演规则
├── 📄 profile.md                # 角色身份与核心标签
├── 📄 personality.md            # 性格、动机与价值观
├── 📄 interaction.md            # 互动语气与台词风格（含50+台词样本）
├── 📄 memory.md                 # 背景故事与剧情梳理
├── 📄 background_story.md       # 原始背景故事整合
├── 📄 relations.md              # 关系网络与人物联动
├── 📄 conflicts.md              # 设定冲突与保守表述
├── 📄 manifest.json             # 元数据与质量评估
├── 📄 quality-report.md         # 质量评估详细报告
├── 📄 roleplay-test-report.md   # 角色扮演测试结果
└── 📄 LICENSE                   # 开源许可证
```

## 🎭 角色设定详解

### 核心特征

- **身份**: 记忆系角色，温柔而坚韧
- **主题**: 记忆、故事、涟漪、光、种子
- **语气**: 诗意但不空洞，亲近但有界限

### 语言风格要点

#### ✅ 应该表现
- 使用诗意的意象和隐喻
- 保持温柔但不软弱的语气
- 在沉重话题中展现希望
- 对不同关系对象有层次感

#### ❌ 应该避免
- 机械式的分析回答
- 粗鄙或讽刺的语气
- 轻佻地谈论严肃主题
- 过度甜化的表演

### 典型台词模式

```
意象 + 情感 + 邀请
示例："记忆就像水面的涟漪，轻轻扩散...伙伴想听听这个故事吗？"

故事 + 感悟 + 展望
示例："那段往事虽然带着伤痛，但它教会了人家珍惜现在。明天，一定会更好吧？"
```

## 🔧 开发指南

### 扩展角色设定

如果你想添加新的角色特征或台词：

1. **编辑 `interaction.md`** - 添加新的台词样本
2. **更新 `personality.md`** - 扩展性格描述
3. **修改 `relations.md`** - 添加新的关系设定

### 集成到自定义系统

```python
# 示例：自定义集成
class ElysiaSkill:
    def __init__(self):
        self.profile = self.load_file("profile.md")
        self.personality = self.load_file("personality.md")
        self.interactions = self.load_file("interaction.md")
    
    def generate_response(self, user_input, context):
        # 实现你的响应生成逻辑
        # 参考interaction.md中的台词风格
        return self.style_response(raw_response)
```

### 性能优化建议

- 预加载角色数据到内存
- 使用缓存机制存储常用响应
- 实现响应模板系统提高效率

## 🤝 贡献指南

我们欢迎社区贡献！以下是参与方式：

### 如何贡献

1. **报告问题**
   - 在Issues中报告bug或提出改进建议
   - 包含详细的复现步骤和期望结果

2. **提交代码**
   - Fork本项目
   - 创建功能分支 (`git checkout -b feature/AmazingFeature`)
   - 提交更改 (`git commit -m 'Add some AmazingFeature'`)
   - 推送到分支 (`git push origin feature/AmazingFeature`)
   - 开启Pull Request

### 贡献规范

- 遵循现有的代码风格和文档格式
- 确保所有更改都经过测试
- 更新相关文档和示例
- 添加有意义的提交信息

### 需要帮助的领域

- [ ] 补充更多官方语音台词
- [ ] 添加多语言支持
- [ ] 创建更多使用示例
- [ ] 优化性能测试

## 📊 质量报告

### 评估结果

| 指标 | 得分 | 说明 |
|------|------|------|
| 完整性 | 1.0/1.0 | 角色设定覆盖全面 |
| 证据比例 | 0.89/1.0 | 89%内容有可靠来源 |
| 冲突检测 | 0.8/1.0 | 设定一致性良好 |
| 测试通过率 | 0.76/1.0 | 角色扮演测试表现优秀 |
| **总体评分** | **0.88/1.0** | **优秀** |

### 测试场景表现

- ✅ 初次见面场景：0.95分
- ✅ 日常闲聊：0.90分  
- ✅ 核心话题触发：0.88分
- ✅ 情绪表达：0.84-0.90分
- ✅ 关系互动：0.86分

详细测试报告见 [roleplay-test-report.md](roleplay-test-report.md)

## 📄 许可证

本项目采用 [MIT 许可证](LICENSE)。


## 🙏 致谢

### 数据来源

- [萌娘百科 - 昔涟](https://zh.moegirl.org.cn/昔涟(崩坏：星穹铁道))
- [BWiki - 星穹铁道](https://wiki.biligame.com/zzz/)
- 游戏内剧情和语音台词
- 社区玩家整理资料

### 特别感谢

- 《崩坏：星穹铁道》开发团队创造了如此丰富的角色
- 社区玩家提供的宝贵资料和分析
- 所有为这个项目做出贡献的开发者

## 🔗 相关链接

- [官方游戏官网](https://hsr.hoyoverse.com/)
- [问题反馈](https://github.com/HeartEase1/elysia.skill/issues)
- [QQ交流群](https://qun.qq.com/universal-share/share?ac=1&authKey=5skdtKxil5%2BtFnO0S9R4K%2FoHiLOclik9vtXNHF%2BAGFYnw8kVtk7EysBi8VHg2Vsw&busi_data=eyJncm91cENvZGUiOiIxMDE5MjQxNjM3IiwidG9rZW4iOiJzV3Q4aW12Q2F2eGZUblRIK0ViSWhrQlM2Wk4vOGN6TVlxWEhFcTQ1L2o1bUFTZGdZSHA1d3BJc1FKdllLNENaIiwidWluIjoiMzUzNTE0NzUzNCJ9&data=t2ojEYbJkZWVKVyD5mVGG1MCEdpTqqucgR5FW-AksLwrKjHt8GZKgup3cvg9NU3f692-0stZsybBp6lyU4ohpg&svctype=4&tempid=h5_group_info)

---

⭐ 如果这个项目对你有帮助，请给我们一个Star！

💬 有任何问题或建议，欢迎在Issues中讨论！
