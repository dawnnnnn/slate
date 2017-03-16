# Notes 笔记

你可以创建一个 `Note` 对象为自己做记录。`Note`是个笔记对象，笔记的主要信息都存储在这个对象中，可以通过发起记笔记请求来创建一个新的 `Note` 对象，也可以随时查询一个或多个 `Note` 对象的信息。每个 `Note` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的笔记对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**shortUrl** | String | 短链接 | 
**title** | String | 笔记的标题，一句话简洁概括笔记的主要内容 |
**currentStatus** | String | 笔记当前状态，共有 5 种 (`available` 可用的，`pending` 审核中，`rejected` 被拒绝，`recommend` 被推荐的，`deleted` 已删除 )|
**language** | String | 笔记的记录格式 |
**createdDate** | String | 根据 `created` 解析的时间 |
**excerpt** | String | 笔记的摘录，将除文字外的特殊片段转为文字描述，如{代码...} |
**originalText** | String | 笔记主体部分的原文，即题主提问时撰写的原文 |
**parsedText** | String | 解析为 HTML 后的笔记主体部分 |
**forks** | Int | 该笔记的 `fork` 数 |
**likes** | Int | 该笔记的点赞数 |
**comments** | Int | 该笔记的评论数，结果 = 评论笔记数 + 回复评论数 |
**favorites** | Int | 该笔记的收藏数，即多少名用户收藏了该笔记 |
**views** | Int | 该笔记的查看次数 |
**isLiked** | Bool | 表示查看该笔记的用户是否赞同该笔记，未登录查看默认状态为 `false` |
**isPrivated** | Bool | 表示该笔记是否为非公开的私有笔记，`true` 时仅用户自己可见 |
**isFollowed** | Bool | 表示查看该笔记的用户是否关注了该笔记，未登录查看默认状态为 `false` |
**isFavorited** | Bool | 表示查看该笔记的用户是否收藏了该笔记，未登录查看默认状态为 `false` |
**isSelf** | Bool | 是否为当前查看用户自己的笔记，未登录查看默认状态为 `false` |
**isForked** | Bool | 表示当前查看用户是否已 `fork` 此笔记 |
**forkedFrom** | Object | fork笔记的原笔记对象，若为原创笔记则为空 |
**user** | Object | 创建该笔记的用户对象 |
**commentsDetail** | Array | 该笔记下所有回答列表 |

## 查看笔记列表 [/notes] [GET]

>  返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1330000008703409",
		"title": "正则表达式规则",
		"url": "/n/1330000008703409",
		"excerpt": 
		  "```\n表1.常用的元字符 \n代码\t说明\n.\t匹配除换行符以外的任意字符\n\\w\t匹配字母或数字或下划线或汉字\n\\s\t匹配任意的空白符",
		"language": "markdown",
		"createdDate": "1 分钟前",
		"forks": "0",
		"favorites": "0",
		"isPrivate": false,
		"user": {
		  "name": "testoopser",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_big64",
		  "url": "/u/testoopser"
		}
	  },
	  ...
	]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 问题列表类型，共 1 种，`newest`：最新 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 记笔记 [/notes] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1330000008703409",
	"title": "正则表达式规则",
	"url": "/n/1330000008703409",
	"shortUrl": "http://sfau.lt/cjKGjJ",
	"language": "markdown",
	"currentStatus": "available",
	"createdDate": "刚刚",
	"isPrivate": false,
	"isFavorited": false,
	"isSelf": true,
	"isForked": false,
	"views": "0",
	"favotites": "0",
	"forks": 0,
	"comments": "0",
	"excerpt": 
	  "```\n表1.常用的元字符 \n代码\t说明\n.\t匹配除换行符以外的任意字符\n\\w\t匹配字母或数字或下划线或汉字\n\\s\t匹配任意的空白符",
	"parsedText": 
	  "\n<pre><code>表1.常用的元字符 \n代码    说明\n.    匹配除换行符以外的任意字符\n\\w    匹配字母或数字或下划线或汉字\n\\s    匹配任意的空白符\n\\d    匹配数字\n\\b    匹配单词的开始或结束\n^    匹配字符串的开始\n$    匹配字符串的结束\n\n表2.常用的限定符\n代码/语法    说明\n*    重复零次或更多次\n+    重复一次或更多次\n?    重复零次或一次\n{n}    重复n次\n{n,}...",
	"user": {
	  "id": "1030000004958804",
	  "name": "testoopser",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_big64",
	  "ranks": "0",
	  "url": "/u/testoopser",
	  "followers": 1,
	  "isFollowed": false,
	  "slug": "testoopser",
	},
	"forkedNote": {},
	"commentsDetail": []
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**title** | String | 笔记的标题，一句话概括该笔记的主要内容 |
**language** | String | 笔记的记录格式，共 12 种 （`text`, `markdown`, `javascript`, `css`, `html`, `php`, `python`, `ruby`, `go`, `c/c++`, `java`, `shell/bash`） |
**text** | String | 笔记的主体部分 | 
**isPrivate** | Bool | 是否公开此笔记 | 

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改笔记 [/notes] [PUT]

请求参数 | | |
-------------- | -------------- | -------------- |
**noteId** | String | 笔记的唯一 id |
**title** | String | 笔记的标题，一句话概括该笔记的主要内容 |
**language** | String | 笔记的记录格式，共 12 种 （`text`, `markdown`, `javascript`, `css`, `html`, `php`, `python`, `ruby`, `go`, `c/c++`, `java`, `shell/bash`） |
**text** | String | 笔记的主体部分 | 
**isPrivate** | Bool | 是否公开此笔记 | 

<aside class="notice">
只有登录用户，并且当前笔记所有者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除笔记 [/notes] [DELETE]

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
**noteId** | String | 笔记的唯一 id |

<aside class="notice">
只有登录用户，并且当前笔记所有者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 笔记详情 [/notes/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1330000008703409",
	"title": "正则表达式规则",
	"url": "/n/1330000008703409",
	"shortUrl": "http://sfau.lt/cjKGjJ",
	"language": "markdown",
	"currentStatus": "available",
	"createdDate": "6 分钟前",
	"isPrivate": false,
	"isFavorited": false,
	"isSelf": true,
	"isForked": false,
	"views": "0",
	"favotites": "0",
	"forks": 0,
	"comments": "0",
	"excerpt": 
	  "```\n表1.常用的元字符 \n代码\t说明\n.\t匹配除换行符以外的任意字符\n\\w\t匹配字母或数字或下划线或汉字\n\\s\t匹配任意的空白符",
	"parsedText": 
	  "\n<pre><code>表1.常用的元字符 \n代码    说明\n.    匹配除换行符以外的任意字符\n\\w    匹配字母或数字或下划线或汉字\n\\s    匹配任意的空白符\n\\d    匹配数字\n\\b    匹配单词的开始或结束\n^    匹配字符串的开始\n$    匹配字符串的结束\n\n表2.常用的限定符\n代码/语法    说明\n*    重复零次或更多次\n+    重复一次或更多次\n?    重复零次或一次\n{n}    重复n次\n{n,}...",
	"user": {
	  "id": "1030000004958804",
	  "name": "testoopser",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_big64",
	  "ranks": "0",
	  "url": "/u/testoopser",
	  "followers": 1,
	  "isFollowed": false,
	  "slug": "testoopser",
	},
	"forkedNote": {
	  "id": "1330000008679787",
	  "title": "正则表达式规则",
	  "url": "/n/1330000008679787",
	  "user": {
		"name": "littlelightss",
		"slug": "littlelightss",
		"url": "/u/littlelightss"
	  }
	},
	"commentsDetail": ""
  }
}
```

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 笔记评论列表 [/notes/{id}/comments] [GET]

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
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 评论笔记 [/notes/{id}/comments] [POST]

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

## 删除笔记评论 [/notes/{id}/comments] [DELETE]

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

## fork笔记 [/notes/{id}/forks] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1330000008703409",
	"url": "/n/1330000008703409"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 收藏笔记 [/notes/{id}/likes] [POST]

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

## 举报笔记 [/notes/{id}/report] [POST]

> Response示例

``` json
{
  "status": 0,
  "message": "感谢您为社区做出的贡献！",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**reason** | String | 举报问题的原因，共 4 种 （`垃圾信息`, `违规内容`, `不友善内容`, `内容质量差`） |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>


