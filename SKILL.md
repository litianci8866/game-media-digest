---
name: game-media-digest
description: 游戏行业媒体日报生成器。每日抓取游戏葡萄、游戏陀螺、手游那点事、游戏新知（国内行业）、白鲸出海、Sensor Tower中国、伽马数据（出海动态）、GamesIndustry.biz、Pocket Gamer、Game Developer（海外行业）的最新文章，整理成三个板块的日报发送到飞书。有内容则推送，无内容则不推送。触发关键词：游戏媒体日报、行业媒体、游戏媒体摘要。
---

# 游戏行业媒体日报

## 任务目标

抓取 10 家游戏行业媒体过去 24 小时发布的文章，提炼要点，整理成三个板块（国内行业 / 出海动态 / 海外行业）发送到飞书。

重点关注：
- 行业重大新闻（厂商动态、财报、融资、裁员并购）
- 产品分析与数据解读
- 市场趋势与洞察报告
- 出海市场动态与数据
- 海外主要游戏公司、平台、市场动向

**不收录**：纯广告软文、招聘资讯、无实质内容的活动通知、游戏评测（IGN等媒体的单纯评分评测文章）。

---

## 媒体来源

详见 [references/sources.md](references/sources.md)。

**国内行业板块**：游戏葡萄、游戏陀螺、手游那点事、游戏新知

**出海动态板块**：白鲸出海、Sensor Tower中国、伽马数据

**海外行业板块**：GamesIndustry.biz、Pocket Gamer、Game Developer

---

## 执行步骤

### 第一步：确定时间范围

今日日期及过去 24 小时范围。严格过滤，只收录该时间窗口内发布的内容。

### 第二步：逐源抓取

每个来源按以下策略抓取，抓完一家立即记录结果再进行下一家。国内来源和海外来源可并行抓取。

#### 国内行业板块

**游戏陀螺**（WebFetch，直接可用）
```
WebFetch: https://www.youxituoluo.com/
```
从文章列表中筛选发布时间在过去 24 小时内的文章。

**游戏葡萄**（WebFetch TapTap 官方论坛）
```
WebFetch: https://www.taptap.cn/forum/g162660
```
筛选 24 小时内的帖子，TapTap 链接作为原文链接。

**手游那点事**（官网国内IP限制，走 WebSearch）
```
WebSearch: 手游那点事 游戏 {今日日期}
```
备用：搜索 36kr 同步版本 `site:36kr.com 手游那点事 {今日日期}`

**游戏新知**（官网国内IP限制，走 WebSearch）
```
WebSearch: site:youxixinzhi.com {今日日期}
```

#### 出海动态板块

**白鲸出海**（WebSearch + site 过滤）
```
WebSearch: site:baijing.cn {今日日期}
```

**Sensor Tower中国**（WebSearch + site 过滤）
```
WebSearch: site:sensortower.com/zh-cn {今日日期}
```
注：每周 2-4 篇，非每日更新，无内容直接跳过。

**伽马数据**（WebSearch）
```
WebSearch: 伽马数据 游戏报告 {今日日期}
```
注：月/季度级报告，多数日期无内容，无内容直接跳过。

#### 海外行业板块

**GamesIndustry.biz**（WebFetch RSS，最稳定）
```
WebFetch: https://www.gamesindustry.biz/feed
```
解析 RSS XML，筛选 24 小时内的条目。备用：`WebFetch: https://www.gamesindustry.biz/`

**Pocket Gamer**（WebFetch RSS）
```
WebFetch: https://www.pocketgamer.biz/feed/
```
解析 RSS XML，筛选 24 小时内的条目。备用：`WebFetch: https://www.pocketgamer.biz/`

**Game Developer**（WebFetch RSS）
```
WebFetch: https://www.gamedeveloper.com/rss.xml
```
解析 RSS XML，筛选 24 小时内的条目。定位：开发者向深度内容，GDC 报道、研发方法论、行业洞察。

### 第三步：内容筛选与提炼

每篇文章提炼：
- 一句话标题（保留核心信息，去除营销语气；海外媒体文章翻译成中文）
- 2-3 个关键点（数据、结论、事件）
- 原文链接

每家媒体最多收录 **3 篇**最重要的文章，按重要性排序。

### 第四步：按模板生成日报

参考 [references/template.md](references/template.md) 生成最终输出。

### 第五步：发送到飞书

有内容时，将日报写入临时文件，通过飞书自定义机器人 Webhook 发送：

```bash
# 写入临时文件
cat > /tmp/game_media_digest.txt << 'EOF'
{日报内容}
EOF

# 通过飞书 Webhook 发送（将 YOUR_WEBHOOK_URL 替换为你的 Webhook 地址）
python3 -c "
import urllib.request, json, sys
content = open('/tmp/game_media_digest.txt').read()
data = json.dumps({'msg_type': 'text', 'content': {'text': content}}).encode()
req = urllib.request.Request('YOUR_WEBHOOK_URL', data=data, headers={'Content-Type': 'application/json'})
urllib.request.urlopen(req)
print('发送成功')
"
```

**配置说明：**
- 在飞书群组中添加「自定义机器人」，获取 Webhook URL
- 将上方 `YOUR_WEBHOOK_URL` 替换为实际地址
- 也可将发送逻辑封装为本地脚本，在此处调用

所有来源均无 24 小时内内容时，不生成日报，不发送。
