# Shares 分享/头条

你可以创建一个 `Share` 对象向用户分享。`Question`是个头条对象，所有头条的主要信息都存储在这个对象中，可以通过发起创建头条请求来创建一个新的 `Share` 对象，也可以随时查询一个或多个 `Share` 对象的信息。每个 `Share` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**title** | String | 头条的标题，多为原链接标题，可由用户在创建时自行更改 |
**currentStatus** | String | 问题当前状态，共有 5 种 (`available` 可用的，`deleted` 已删除 )|
**host** | String | 头条出处的 Host |
**originUrl** | String | 头条出处的原url |
**desc** | String | 分享该头条时，用户的推荐语 |
**type** | String | 头条的类型，共 2 种（ `url` 链接头条，`text` 文本头条） |
**channel** | Srting | 头条的频道，共 9 种 () |
**parsedText** | String | 重新解析排版后的头条主体部分 |
**originalText** | String | 头条解析后的纯文本主体部分 |
**createdDate** | String | 根据 `created` 解析的时间 |
**thumbnailUrl** | String | 带缩略图头条的图片链接 |
**views** | Int | 该分享的阅读数 |
**likes** | Int | 该分享的点赞数 |
**comments** | Int | 该问题的评论数，结果 = 评论问题数 + 回复评论数 |
**favorites** | Int | 该问题的收藏数，即多少名用户收藏了该问题 |
**isLiked** | Bool | 表示查看该问题的用户是否赞同该问题，未登录查看默认状态为 `false` |
**isFavorited** | Bool | 表示查看该问题的用户是否收藏了该问题，未登录查看默认状态为 `false` |
**user** | Object | 分享该头条的用户对象 |

## 头条列表 [/shares] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
		"id": "1210000008691272",
		"title": "一位月收入7000开发者的技术选型",
		"url": "/p/1210000008691272",
		"description": 
		  "\n<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n<p>所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。</p>\n",
		"currentStatus": "available",
		"likes": "3",
		"comments": "0",
		"createdDate": "4 小时前",
		"isLiked": false,
		"thumbnailUrl": null,
		"type": "url",
		"user": {
		  "id": "1030000002377284",
		  "name": "利维坦少女",
		  "url": "/u/catscarlet",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/255/540/2555403060-55d8ba52c6b94_big64"
		},
		"channel": "程序员"
	  },
	  ...
    ]
  }
}
```

根据指定 `type` 返回一个 `Share` 对象的列表。列表排序方式由用户自主选择。

请求参数 | | |
-------------- | -------------- | -------------- |
**sort** | String | 问题列表类型，共3种，`hottest`：最热，`newest`：最新 |
**channel** _optional_| String | type 为 `tag` 时必传，填写 tag 的 slug 或者 id |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 发布头条 [/shares] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1210000008691272",
	"title": "一位月收入7000开发者的技术选型",
	"host": "blog.catscarlet.com",
	"url": "/p/1210000008691272",
	"desc": 
	  "\n<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n<p>所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。</p>\n",
	"currentStatus": "available",
	"views": "1",
	"likes": "0",
	"comments": "0",
	"favorites": "0",
	"type": "url",
	"channel": "程序员"
	"createdDate": "刚刚",
	"isLiked": false,
	"isFavorited": false,
	"parsedText": 
	  "<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n\n<p>以下推荐，除了云服务是一直要收费的外，其他在开发要求中均是免费的服务。</p>\n<h2 id=\"-\">公司级</h2>\n<h3 id=\"-\">技术相关</h3>\n<table>\n<thead><tr>\n<th>类型</th>\n<th>选择</th>\n<th>理由</th>\n</tr></thead>\n<tbody>\n<tr>\n<td>后台语言</td>\n<td>PHP 7</td>\n<td>因为其他后端语言我不熟QAQ</td>\n</tr>\n<tr>\n<td>数据库</td>\n<td>Mysql/Mariadb</td>\n<td>用法一样</td>\n</tr>\n<tr>\n<td>缓存</td>\n<td>Redis</td>...",
	"originUrl": "https://blog.catscarlet.com/201703142751.html",
	"originalText": "昨天看到有人在研究技术选型，于是自己也写了一个列表。\r\n\r\n所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。",
	"thumbnailUrl": null,
	"user": {
	  "id": "1030000002377284",
	  "name": "利维坦少女",
	  "url": "/u/catscarlet",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/255/540/2555403060-55d8ba52c6b94_big64",
	  "isFollowed": false
	}
  }
}
```

发起创建 `Share` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**url** | String | 想要分享的 `url`   |
**channel**  | String  | 分享的链接所属的频道，共 8 种 （`前端`, `后端`, `iOS`, `Android`, `安全`, `工具`, `程序员`, `行业`） |
**desc** _optional_ | String | 分享该头条时用户的描述与见解 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改头条 [/shares] [PUT]

> 示例参见发布头条

请求参数 | | |
-------------- | -------------- | -------------- |
**shareId** | String |  |
**url** | String | 想要分享的 `url`   |
**channel**  | String  | 分享的链接所属的频道，共 8 种 （`前端`, `后端`, `iOS`, `Android`, `安全`, `工具`, `程序员`, `行业`） |
**desc** _optional_ | String | 分享该头条时用户的描述与见解 |

<aside class="notice">
只有登录用户且为头条发布者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除头条 [/shares] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**shareId** | String | 

<aside class="notice">
只有登录用户且为头条发布者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 爬取头条 [/shares/spider] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"titile": "百度一下，你就知道",
	"url": "http://www.baidu.com"
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**url** | String | 想要抓取解析的 `url`   |

## 头条详情 [/shares/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1210000008691272",
	"title": "一位月收入7000开发者的技术选型",
	"host": "blog.catscarlet.com",
	"url": "/p/1210000008691272",
	"desc": 
	  "\n<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n<p>所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。</p>\n",
	"currentStatus": "available",
	"views": "549",
	"likes": "20",
	"comments": "11",
	"favorites": "51",
	"type": "url",
	"channel": "程序员"
	"createdDate": "20 小时前",
	"isLiked": false,
	"isFavorited": false,
	"parsedText": 
	  "<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n\n<p>以下推荐，除了云服务是一直要收费的外，其他在开发要求中均是免费的服务。</p>\n<h2 id=\"-\">公司级</h2>\n<h3 id=\"-\">技术相关</h3>\n<table>\n<thead><tr>\n<th>类型</th>\n<th>选择</th>\n<th>理由</th>\n</tr></thead>\n<tbody>\n<tr>\n<td>后台语言</td>\n<td>PHP 7</td>\n<td>因为其他后端语言我不熟QAQ</td>\n</tr>\n<tr>\n<td>数据库</td>\n<td>Mysql/Mariadb</td>\n<td>用法一样</td>\n</tr>\n<tr>\n<td>缓存</td>\n<td>Redis</td>...",
	"originUrl": "https://blog.catscarlet.com/201703142751.html",
	"originalText": "昨天看到有人在研究技术选型，于是自己也写了一个列表。\r\n\r\n所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。",
	"thumbnailUrl": null,
	"user": {
	  "id": "1030000002377284",
	  "name": "利维坦少女",
	  "url": "/u/catscarlet",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/255/540/2555403060-55d8ba52c6b94_big64",
	  "isFollowed": false
	}
  }
}
```

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 头条评论列表 [/shares/{id}/comments] [GET]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "id": 1050000008644845,
        "likes": "0",
        "replies": "2",
        "isLiked": false,
        "createdDate": "2 天前",
        "originalText":
          "我现在找前端开发工作，到处碰壁，经验不够，人家根本不要，看了你的信息，我更有自信，谢谢你的文章。",
        "parsedText": 
          "<p>我现在找前端开发工作，到处碰壁，经验不够，人家根本不要，看了你的信息，我更有自信，谢谢你的文章。</p>",
        "user": {
          "id": "1030000007653230",
          "url": "/u/wei_hq",
          "slug": "wei_hq",
          "name": "行走的程序猿",
          "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/307/754/3077547314-58b0dd1c62747_medium40"
        }
        "repliedComments": [
		      {
            "id": "1050000008655655",
            "likes": "0",
            "isLiked": false,
            "createdDate": "1 天前",
            "originalText": "@行走的程序猿 找到了吗？",
            "parsedText": "<p>@行走的程序猿 找到了吗？</p>",
            "user": {
              "id": "1030000008273661",
              "url": "/u/luofangyong",
              "slug": "luofangyong",
              "name": "lofy",
              "avatarUrl": "https://sf-static.b0.upaiyun.com/global/img/user-40.png"
            }
          },
          ...
        ]
      },
      ...
    ]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

返回说明 | | |
-------------- | -------------- | -------------- |
**originalText** | String | 评论主体部分的原文，即评论者回答时撰写的原文 |
**parsedText** | String | 解析为 HTML 后的评论主体部分 |
**replies** | Int | 该评论的回复数 |
**repliedComments** | Array | 该评论的回复列表，最多返回 3 项，如有超过 3 项回复，需另外发起请求 |
**isLiked** | Bool | 表示查看该评论的用户是否为该评论点赞，未登录查看默认状态为 `false` |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 评论头条 [/shares/{id}/comments] [POST]


> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": 1050000008644845,
	"likes": "0",
  "replies": "0",
	"isLiked": false,
	"createdDate": "刚刚",
	"originalText":
	  "我现在找前端开发工作，到处碰壁，经验不够，人家根本不要，看了你的信息，我更有自信，谢谢你的文章。",
	"parsedText": 
	  "<p>我现在找前端开发工作，到处碰壁，经验不够，人家根本不要，看了你的信息，我更有自信，谢谢你的文章。</p>",
	"user": {
      "id": "1030000007653230",
      "url": "/u/wei_hq",
      "slug": "wei_hq",
      "name": "行走的程序猿",
      "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/307/754/3077547314-58b0dd1c62747_medium40"
	},
	"repliedComments": []
  }
}
```

发起创建 `Comment` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**text** | String | 评论的内容，限制长度? |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除头条评论 [/shares/{id}/comments] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**commentId** | String | 评论的 id |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 点赞头条 [/shares/{id}/likes] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": true,
    "likes": "3"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消点赞头条 [/shares/{id}/likes] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": false,
    "likes": "2"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 收藏头条 [/shares/{id}/favorites] [POST]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFavorited": true,
    "favorites": 2
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**favoriteIds** | Array | 存入的收藏夹的 `id`，可同时存入多个收藏夹 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>






