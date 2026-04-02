# 游戏行业媒体来源配置

## 国内行业板块

### 游戏葡萄
| 项目 | 内容 |
|------|------|
| 官网 | https://www.youxiputao.com/ |
| TapTap论坛 | https://www.taptap.cn/forum/g162660 |
| 抓取方式 | WebFetch TapTap官方论坛（已验证可用，官网JS渲染无法直接抓） |
| 定位 | 泛游戏行业，深度报道、数据分析 |
| 更新频率 | 每日 3-8 篇 |

### 游戏陀螺
| 项目 | 内容 |
|------|------|
| 官网 | https://www.youxituoluo.com/ |
| 抓取方式 | WebFetch 直接抓取（已验证可用） |
| 定位 | 行业动态、商业分析、创业方向 |
| 更新频率 | 每日 3-6 篇 |

### 手游那点事
| 项目 | 内容 |
|------|------|
| 官网 | http://www.nadianshi.com/ |
| RSS | https://www.nadianshi.com/category/our/feed |
| 抓取方式 | WebSearch: `手游那点事 游戏 {日期}`，备用：`site:36kr.com 手游那点事 {日期}` |
| 备注 | 官网服务器拒绝境外IP连接，走搜索引擎或36kr同步 |
| 定位 | 移动游戏新闻、运营案例 |
| 更新频率 | 每日 2-5 篇 |

### 游戏新知
| 项目 | 内容 |
|------|------|
| 官网 | http://www.youxixinzhi.com/ |
| 文章列表 | http://www.youxixinzhi.com/?cat=96 |
| 抓取方式 | 优先 WebFetch，失败则 WebSearch: `site:youxixinzhi.com {日期}` |
| 定位 | 产品分析、行业洞察，偏深度 |
| 更新频率 | 每日 1-3 篇 |

---

## 出海动态板块

### 白鲸出海
| 项目 | 内容 |
|------|------|
| 官网 | https://www.baijing.cn/ |
| 文章页 | https://www.baijing.cn/article |
| 抓取方式 | WebSearch: `site:baijing.cn {日期}` |
| 定位 | 泛互联网出海，游戏出海为重点方向 |
| 更新频率 | 每日 5-10 篇 |

### Sensor Tower 中国
| 项目 | 内容 |
|------|------|
| 博客 | https://sensortower.com/zh-cn/blog |
| 抓取方式 | WebSearch: `site:sensortower.com/zh-cn {日期}` |
| 定位 | 出海数据报告、榜单分析（Sensor Tower 官方中文内容） |
| 更新频率 | 每周 2-4 篇，非每日 |
| 备注 | 无内容时直接跳过，不强行填充 |

### 伽马数据
| 项目 | 内容 |
|------|------|
| 官网 | http://www.gammadata.cn |
| 抓取方式 | WebSearch: `伽马数据 游戏报告 {日期}` |
| 定位 | 中国游戏产业权威数据报告 |
| 更新频率 | 月/季度级，多数日期无内容 |
| 备注 | 无内容时直接跳过 |

---

## 海外行业板块

### GamesIndustry.biz
| 项目 | 内容 |
|------|------|
| 官网 | https://www.gamesindustry.biz/ |
| RSS | https://www.gamesindustry.biz/feed |
| 抓取方式 | WebFetch RSS（已验证境外IP可访问） |
| 定位 | 游戏行业商业媒体，并购融资、财报、厂商动态、市场数据 |
| 更新频率 | 每日 5-15 篇 |
| 备注 | 优先收录商业/行业新闻，跳过纯评测 |

### Pocket Gamer（Business版）
| 项目 | 内容 |
|------|------|
| 官网 | https://www.pocketgamer.biz/ |
| RSS | https://www.pocketgamer.biz/feed/ |
| 抓取方式 | WebFetch RSS（已验证境外IP可访问） |
| 定位 | 手游行业商业媒体，移动市场分析、下载收入榜单、开发者动态 |
| 更新频率 | 每日 3-8 篇 |

### Game Developer（原 Gamasutra）
| 项目 | 内容 |
|------|------|
| 官网 | https://www.gamedeveloper.com/ |
| RSS | https://www.gamedeveloper.com/rss.xml |
| 抓取方式 | WebFetch RSS（已验证境外IP可访问） |
| 定位 | 开发者向深度媒体，GDC 报道、研发方法论、行业洞察、技术趋势 |
| 更新频率 | 每日 5-10 篇 |
| 备注 | IGN 对 Claude 服务器完全屏蔽，已移除 |
