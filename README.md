# 微信数据接口：公众号文章、阅读数、视频号、微信搜一搜

**公众号文章接口 · 公众号历史文章 · 公众号阅读数在看数 · 视频号数据 API · 微信搜一搜 · 微信指数。**

这个仓库是 [okdata](https://okdata.online/zh/?src=gh-wechat-api) 的微信公众号、微信视频号、微信搜一搜接口示例：29 个接口在线可用，一个 API Key 调用，按次计费（$0.015 起），不用订阅。不用登录平台账号，不用 Cookie，不开浏览器，所以也不存在账号被风控的问题。

[免费注册拿 Key（送 $0.1 试用额度）](https://okdata.online/zh/signup/?src=gh-wechat-api) · [全部接口文档](https://okdata.online/zh/apis/?src=gh-wechat-api) · [接入 AI（MCP）](https://okdata.online/zh/mcp/?src=gh-wechat-api)

## 接口清单

### 微信公众号

| 接口 | 说明 | 价格 | 路径 |
|---|---|---|---|
| [公众号搜索](https://okdata.online/zh/apis/wechat_mp/accounts/search/) | 按名称或关键词找公众号，返回原始 ID（gh_…）。按返回的账号数计费；余额不够一整页时，第一页按余额能付的条数返回。 | 每条 $0.058（最少 $0.058） | `GET /v1/wechat_mp/accounts/search` |
| [公众号历史文章](https://okdata.online/zh/apis/wechat_mp/accounts/articles/list/) | 公众号已发布的文章，从新到旧，不用扫码登录：默认是主页的“文章”栏，也可取“视频”或“贴图”栏。 | $0.02 / 次 | `GET /v1/wechat_mp/accounts/articles/list` |
| [公众号文章详情](https://okdata.online/zh/apis/wechat_mp/articles/get/) | 文章全文（纯文本），带公众号和发布时间。 | $0.02 / 次 | `GET /v1/wechat_mp/articles/get` |
| [公众号资料](https://okdata.online/zh/apis/wechat_mp/accounts/get/) | 按原始 ID 取公众号资料：名称、IP 属地、原创文章数、关联的视频号和是否被封禁。这里微信不给简介、头像和粉丝数。 | $0.02 / 次 | `GET /v1/wechat_mp/accounts/get` |
| [公众号文章评论](https://okdata.online/zh/apis/wechat_mp/articles/comments/list/) | 按文章链接取公众号文章的精选评论：内容、评论者、点赞、回复数、发布时间、IP 属地和是否置顶。评论的 id 可传给 wechat_mp.comments.replies.list 取回复。 | $0.02 / 次 | `GET /v1/wechat_mp/articles/comments/list` |
| [公众号文章互动数据](https://okdata.online/zh/apis/wechat_mp/articles/metrics/) | 按文章链接取这篇文章此刻的数字：阅读、点赞、在看（ext.recommends）、分享、收藏和评论。只有数字：标题和正文用 wechat_mp.articles.get 取。 | $0.02 / 次 | `GET /v1/wechat_mp/articles/metrics` |
| [公众号评论回复](https://okdata.online/zh/apis/wechat_mp/comments/replies/list/) | 按评论 ID 和文章链接取公众号文章一条评论下面的回复：内容、回复者、点赞、发布时间和 IP 属地。只返回第一批，不翻页。 | $0.02 / 次 | `GET /v1/wechat_mp/comments/replies/list` |
| [公众号主体信息](https://okdata.online/zh/apis/wechat_mp/accounts/owner/get/) | 按原始 ID 取公众号背后的主体：公司、机构或个人的名称、类型、登记证照号码和国家或地区，认证状态、认证类型和日期，公众号注册日期，以及授权过的第三方服务商。 | $0.15 / 次 | `GET /v1/wechat_mp/accounts/owner/get` |

### 微信视频号

| 接口 | 说明 | 价格 | 路径 |
|---|---|---|---|
| [视频号视频搜索](https://okdata.online/zh/apis/wechat_channels/videos/search/) | 通过微信搜一搜按关键词搜视频号视频，可按相关、最新或最热排，可按发布时间筛选：描述、账号名称和头像、发布时间、时长和封面（url）。id 是 export/ 开头的加密 ID，传给 wechat_channels.videos.get 可以拿到视频、数字 ID 和账号 ID；它会过期，搜到后尽快用。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/search` |
| [视频号账号搜索](https://okdata.online/zh/apis/wechat_channels/users/search/) | 通过微信搜一搜按名称找视频号账号：账号 ID（v2_…@finder）、名称、头像和认证主体。搜一搜通常只返回名称最匹配的那一个。 | $0.02 / 次 | `GET /v1/wechat_channels/users/search` |
| [视频号账号信息](https://okdata.online/zh/apis/wechat_channels/users/get/) | 按账号 ID 取视频号账号：名称、签名、头像、IP 属地、作品数、累计直播时长和关联的公众号。微信不公开时，粉丝数和获赞数为 null。 | $0.02 / 次 | `GET /v1/wechat_channels/users/get` |
| [视频号账号作品](https://okdata.online/zh/apis/wechat_channels/users/videos/list/) | 账号发布的视频，从新到旧，每页约 15 条：描述、发布时间、点赞、评论、转发和收藏、时长。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/users/videos/list` |
| [视频号作品详情](https://okdata.online/zh/apis/wechat_channels/videos/get/) | 按作品 ID、搜索结果的 export/ 加密 ID 或分享链接取一个视频：描述、作者（含账号 ID）、发布时间、点赞、评论、转发、收藏和位置。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/get` |
| [视频号作品评论](https://okdata.online/zh/apis/wechat_channels/videos/comments/list/) | 视频的一级评论，按热度排：内容、评论者、点赞、回复数、发布时间和 IP 属地。 | $0.015 / 次 | `GET /v1/wechat_channels/videos/comments/list` |
| [视频号评论回复](https://okdata.online/zh/apis/wechat_channels/comments/replies/list/) | 按评论 ID 和所在作品 ID 取一级评论下的回复：内容、回复者、点赞、发布时间和 IP 属地。 | $0.015 / 次 | `GET /v1/wechat_channels/comments/replies/list` |
| [视频号直播回放](https://okdata.online/zh/apis/wechat_channels/users/live_replays/list/) | 账号的直播回放，从新到旧，每页最多约 50 条：标题、时间、点赞、评论和转发。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/users/live_replays/list` |
| [视频号作品分享链接](https://okdata.online/zh/apis/wechat_channels/videos/share_link/get/) | 按作品 ID 生成一条能在微信里打开的分享链接（weixin.qq.com/sph/ 开头）。每次生成的链接都不同，旧链接仍然有效；链接无法用 ID 自己拼出来。 | $0.02 / 次 | `GET /v1/wechat_channels/videos/share_link/get` |
| [视频号账号合集](https://okdata.online/zh/apis/wechat_channels/users/collections/list/) | 视频号账号公开的全部合集，一次返回：名称、简介、封面、视频数和最近更新时间。合集的 id 传给 wechat_channels.collections.videos.list 取里面的视频。 | $0.02 / 次 | `GET /v1/wechat_channels/users/collections/list` |
| [视频号合集视频](https://okdata.online/zh/apis/wechat_channels/collections/videos/list/) | 视频号合集里的视频，按合集自己的顺序（从最早的开始），每页 20 条：描述、账号、发布时间、点赞、评论、转发和收藏、时长。url 是视频文件地址（已加密，用同一次返回的 ext.decode_key 解密）。 | $0.02 / 次 | `GET /v1/wechat_channels/collections/videos/list` |
| [视频号作品互动数据](https://okdata.online/zh/apis/wechat_channels/videos/metrics/) | 按作品 ID 取视频号作品最近的数字：点赞、评论、转发和收藏，带作品描述和发布账号。数字可能是几小时前的，ext.counted_at 写明取数时间。比取整个作品（wechat_channels.videos.get）便宜。 | $0.015 / 次 | `GET /v1/wechat_channels/videos/metrics` |
| [视频号账号信息（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/users/get/) | wechat_channels.users.get 的备用版：参数和返回相同，不给作品数。 | $0.03 / 次 | `GET /v1/wechat_channels/backup/users/get` |
| [视频号账号作品（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/users/videos/list/) | wechat_channels.users.videos.list 的备用版：参数和返回相同，每页 15 条（正在直播时第一条是直播）。 | $0.06 / 次 | `GET /v1/wechat_channels/backup/users/videos/list` |
| [视频号视频搜索（备用版）（备用版）](https://okdata.online/zh/apis/wechat_channels/backup/videos/search/) | wechat_channels.videos.search 的备用版：参数和返回相同，另带评论数和转发数（没有收藏数）。 | $0.15 / 次 | `GET /v1/wechat_channels/backup/videos/search` |

### 微信搜一搜

| 接口 | 说明 | 价格 | 路径 |
|---|---|---|---|
| [微信搜一搜综合搜索](https://okdata.online/zh/apis/wechat/posts/search/) | 按关键词取微信搜一搜结果：公众号文章和视频号视频混排（type 标明是哪种），可按相关、最新或最热排、按发布时间筛，也可只搜文章或只搜视频。标题或描述、来源账号名称、发布时间；文章带链接（部分带阅读数档位），视频带点赞数和可传给 wechat_channels.videos.get 的 export/ 加密 ID。搜一搜不给账号 ID。 | $0.02 / 次 | `GET /v1/wechat/posts/search` |
| [微信公众号实时查找](https://okdata.online/zh/apis/wechat/accounts/search/) | 按关键词在微信搜一搜里实时找公众号和服务号，最像的排前面（后面可能跟着不太相关的）：原始 ID、微信号、名称、简介、头像、是否认证和认证主体、原创文章数。按次计费；不带粉丝和阅读数（要估计值用 wechat_mp.accounts.search）。 | $0.02 / 次 | `GET /v1/wechat/accounts/search` |
| [微信指数](https://okdata.online/zh/apis/wechat/index/keywords/history/) | 关键词最近 30 天的微信指数，一天一个数（points[].composite_index）。微信指数是微信综合搜一搜、文章、朋友圈等算出的热度分，不是搜索次数，不能和抖音、小红书的指数比；日期是中国时间（UTC+8）的自然日。 | $0.15 / 次 | `GET /v1/wechat/index/keywords/history` |
| [微信搜一搜推荐词](https://okdata.online/zh/apis/wechat/keywords/related/) | 微信搜一搜在搜索框下给一个关键词的联想推荐词，按它列出的顺序，一次约 9 个（不含关键词本身）。只有词和名次，没有指数。 | $0.15 / 次 | `GET /v1/wechat/keywords/related` |
| [微信小程序搜索](https://okdata.online/zh/apis/wechat/miniprograms/search/) | 按关键词在微信搜一搜里找小程序，取第一页（约 25 个）：名称、简介、图标、原始 ID 和 AppID（部分品牌小程序不显示）、主体和是否认证、平台显示的最近使用人数（取档位下限，如 10万+ 记为 100000）、是否小游戏。 | $0.15 / 次 | `GET /v1/wechat/miniprograms/search` |
| [微信搜一搜综合搜索（备用版）（备用版）](https://okdata.online/zh/apis/wechat/backup/posts/search/) | wechat.posts.search 的备用版：参数和返回相同。 | $0.15 / 次 | `GET /v1/wechat/backup/posts/search` |

## 快速开始

1. 在 [okdata 控制台](https://okdata.online/zh/signup/?src=gh-wechat-api) 用邮箱注册，拿到 `okd_` 开头的 Key。
2. 调一次接口：

```bash
export OKDATA_API_KEY=okd_...
curl -G "https://api.okdata.online/v1/wechat/posts/search" \
  -H "Authorization: Bearer $OKDATA_API_KEY" \
  --data-urlencode 'query=咖啡店开业'
```

Python 版在 [examples/quickstart.py](examples/quickstart.py)（只用标准库，会顺带演示翻页）：`python3 examples/quickstart.py`。

返回统一的结构：列表在 `data.items`，下一页用 `page.next_cursor` 传回 `cursor`，这次扣了多少钱在 `meta.billing.amount`，平台不提供的字段为 null 并在 `meta.unavailable` 里写明原因。

## 让 AI 直接用（MCP）

Claude Code：

```bash
claude mcp add --transport http --scope user okdata https://api.okdata.online/mcp --header "Authorization: Bearer $OKDATA_API_KEY"
```

Cursor、Cherry Studio、WorkBuddy 等支持远程 MCP 的客户端：

```json
{
  "mcpServers": {
    "okdata": {
      "url": "https://api.okdata.online/mcp",
      "headers": {
        "Authorization": "Bearer okd_..."
      }
    }
  }
}
```

接好以后直接用中文说需求，比如「微信搜一搜综合搜索：咖啡店开业」。AI 会先用免费的 `find`、`describe` 找接口和看价格，再用 `call` 取数据。

## 常见问题

**要登录平台账号吗？** 不用。数据是公开内容，okdata 在服务端获取，你的账号完全不参与。

**怎么收费？** 每个接口单独定价，表里写的就是一次调用的价格；按条计费的接口按实际返回条数算。新账号送 $0.1 试用额度，之后 $10 起充，余额不过期，没有订阅。价格页：https://okdata.online/zh/pricing/ ，计费说明：https://okdata.online/zh/docs/billing/

**和官方开放平台有什么区别？** 官方开放平台只能读授权给你的账号自己的数据，而且要企业资质和审核；这里是平台上任何人都能看到的公开数据，比如搜索结果、别人的笔记或视频、评论、热榜。

**能翻页吗？** 列表接口每页一次调用，把 `page.next_cursor` 原样传回 `cursor` 就是下一页，24 小时内有效。

**出错了怎么办？** 每个错误都有固定的 `code`、中文说明 `message_zh`，以及会不会扣费（`charged`）和要不要重试（`retry`）。全部错误码：https://okdata.online/zh/docs/errors/

## English

Examples for the okdata WeChat Official Accounts, WeChat Channels, WeChat Search API: 29 live endpoints behind one API key, pay per call from $0.015, no platform login or cookies. Sign up at https://okdata.online/signup/?src=gh-wechat-api, docs at https://okdata.online/apis/, MCP at https://okdata.online/mcp/.

## License

MIT. The data comes from the okdata API; its terms apply to API use.
