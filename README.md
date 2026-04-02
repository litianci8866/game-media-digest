# game-media-digest

> 游戏行业媒体日报 · Claude Code Skill
游戏从业者必装的游戏行媒日报skill！每天要打开好几个公众号和网页看行业快讯？海外行媒不知道看哪些密密麻麻英文头疼？这个skill为你而生！精选了国内和海外10家行业媒体，包括游戏葡萄、游戏陀螺、白鲸出海、Sensor Tower中国、GamesIndustry.biz、Pocket Gamer、Game Developer等一线媒体，使用这个SKILL，可以自定义每日x点为你发送行媒摘要，不错过业界重要更新、精简阅读时间！

A must-have daily digest skill for game industry professionals.

Tired of opening multiple sites for industry news? Not fluent in Chinese but want to follow China's gaming market? This skill has you covered.

It aggregates 10 leading outlets across China and the West — YouXiPuTao, YouXiTuoLuo, BaiJing, Sensor Tower China, GamesIndustry.biz, Pocket Gamer, and Game Developer — and delivers a clean three-section digest (domestic / overseas expansion / global) to your Feishu every day.

Set your preferred delivery time. Stay informed without the tab-switching.


每日自动抓取 10 家游戏行业媒体过去 24 小时发布的文章，提炼要点，整理成结构化日报发送到飞书。

---

## 覆盖媒体

| 板块 | 媒体来源 |
|------|---------|
| 国内行业 | 游戏葡萄、游戏陀螺、手游那点事、游戏新知 |
| 出海动态 | 白鲸出海、Sensor Tower 中国、伽马数据 |
| 海外行业 | GamesIndustry.biz、Pocket Gamer、Game Developer |

重点收录：厂商动态、财报融资、产品分析、出海数据、市场趋势。
自动过滤：广告软文、招聘资讯、无实质内容的活动通知、纯游戏评测。

---

## 输出示例

```
Game Media Digest - 2026年04月02日

——国内行业动态——

【游戏陀螺】

1. 自研烧了5亿，《卡拉彼丘》盈利，创梦天地终于回本了
   · 2025年总营收13.38亿元，经调整净利润2亿元扭亏为盈
   · 《卡拉彼丘》投入近5亿元，手游版上线后终于实现盈利
   · AI单日消耗token接近百亿，已覆盖产品全流程
   🔗 https://www.youxituoluo.com/534355.html

——海外行业动态——

【Pocket Gamer】

1. Rec Room宣布关服：1.5亿玩家，却始终烧不平成本
   · 官方坦言"成本始终压过收入"，6月1日停止全部服务
   · VR市场转冷叠加行业整体压力是关键因素
   🔗 https://www.pocketgamer.biz/...
```

---

## 安装

### 1. 下载 Skill

将本仓库克隆或下载到 Claude Code 的 skills 目录：

```bash
# macOS / Linux
git clone https://github.com/你的用户名/game-media-digest.git \
  ~/.claude/skills/game-media-digest

# Windows
git clone https://github.com/你的用户名/game-media-digest.git \
  %USERPROFILE%\.claude\skills\game-media-digest
```

### 2. 配置飞书 Webhook

1. 在飞书群组中点击「设置」→「群机器人」→「添加机器人」→「自定义机器人」
2. 复制生成的 Webhook URL（格式：`https://open.feishu.cn/open-apis/bot/v2/hook/xxxxx`）
3. 打开 `SKILL.md`，将第五步中的 `YOUR_WEBHOOK_URL` 替换为你的 Webhook 地址

> **发送到个人账号**：需使用飞书开放平台 API 或自行封装发送脚本，Webhook 仅支持群消息。

### 3. 验证安装

重启 Claude Code，输入以下任意关键词触发：

```
游戏媒体日报
游戏行媒
游戏媒体摘要
```

或直接运行：

```
/game-media-digest
```

---

## 工作原理

```
触发关键词
    ↓
确定时间范围（过去 24 小时）
    ↓
并行抓取 10 家媒体
  ├─ WebFetch（游戏陀螺、TapTap论坛、海外RSS）
  └─ WebSearch（IP受限的国内媒体）
    ↓
筛选 24h 内文章 → 提炼标题 + 2-3 个关键点
    ↓
按模板生成三板块日报
    ↓
发送到飞书（有内容则推送，无内容则跳过）
```

---

## 抓取策略说明

不同媒体的服务器访问限制不同，skill 针对每家媒体选择了最可靠的抓取方式：

| 媒体 | 方式 | 说明 |
|------|------|------|
| 游戏陀螺 | WebFetch 直接访问 | 服务器对境外IP开放 |
| 游戏葡萄 | WebFetch TapTap论坛 | 官网JS渲染无法抓取，TapTap论坛可用 |
| 手游那点事 | WebSearch | 官网拒绝境外IP，走搜索引擎 |
| 游戏新知 | WebSearch | 同上 |
| 白鲸出海 | WebSearch | JS渲染，走搜索引擎 |
| Sensor Tower | WebSearch | 按需搜索，非每日更新 |
| 伽马数据 | WebSearch | 月/季度级报告，多数日期无内容 |
| GamesIndustry.biz | WebFetch RSS | 境外IP可访问 |
| Pocket Gamer | WebFetch RSS | 境外IP可访问 |
| Game Developer | WebFetch RSS | 境外IP可访问 |

---

## 自定义

### 修改媒体来源

编辑 `references/sources.md`，按现有格式添加或删除媒体条目，并在 `SKILL.md` 第二步中对应增减抓取指令。

### 修改输出格式

编辑 `references/template.md`。

### 调整筛选标准

编辑 `SKILL.md` 中「第三步：内容筛选与提炼」部分。

---

## 文件结构

```
game-media-digest/
├── SKILL.md                  # 主工作流（Claude Code 读取）
├── README.md                 # 本文件
└── references/
    ├── sources.md            # 媒体来源配置与抓取策略
    └── template.md           # 日报输出模板
```

---

## 依赖

- [Claude Code](https://claude.ai/claude-code) — Anthropic 官方 CLI
- 飞书自定义机器人 Webhook（免费）
- Python 3（用于发送飞书消息，系统自带即可）

---

## License

MIT
