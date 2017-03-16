# Comments 评论

你可以创建一个 `Comment` 对象对 `文章` / `问题` / `答案` / `笔记` / `头条` / `活动` 进行评论，也可以对 `Comment`评论 进行回复。每个 `Comment` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**createdDate** | String | 根据 `created` 解析的时间 |
**originalText** | String | 问题主体部分的原文，即题主提问时撰写的原文 |
**parsedText** | String | 解析为 HTML 后的问题主体部分 |
**likes** | Int | 该问题的认可数 |
**replies** | Int | 该评论的回复数 |
**isLiked** | Bool | 表示查看此评论的用户是否为此评论点赞 |
**user** | Object | 创建该问题的用户对象 |
**repliedComments** | Array | 该评论的当前回复数|


## 评论详情 [/comments/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
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
  }
}
```

<aside class="notice">
当前登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 评论点赞 [/comments/{id}/likes] [POST]

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

## 取消评论点赞 [/comments/{id}/likes] [DELETE]

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

## 子评论列表 [/comments/{id}/replies] [GET]

> 返回示例 

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1050000008422052",
		"likes": "2",
		"isLiked": false,
		"originalText": "@oopser \U6765\U554a\U9020\U4f5c\U554a",
		"parsedText": "<p><a href=\"/u/oopser\">@oopser</a> \U6765\U554a\U9020\U4f5c\U554a</p>",
		"createdDate": "2 天前"
		"user": {
		  "id": "1030000005636610",
		  "name": "crisitina",
		  "avartaUrl": "https://sfault-avatar.b0.upaiyun.com/339/576/3395766462-58058db405e0e_medium40",
		  "url": "/u/_natie_"
		}
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

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 回复评论 [/comments/{id}/replies] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1050000008422052",
	"likes": "0",
	"isLiked": false,
	"originalText": "@oopser \U6765\U554a\U9020\U4f5c\U554a",
	"parsedText": "<p><a href=\"/u/oopser\">@oopser</a> \U6765\U554a\U9020\U4f5c\U554a</p>",
	"createdDate": "2 天前"
	"user": {
	  "id": "1030000005636610",
	  "name": "crisitina",
	  "avartaUrl": "https://sfault-avatar.b0.upaiyun.com/339/576/3395766462-58058db405e0e_medium40",
	  "url": "/u/_natie_"
	}
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**text** | String | 回复评论的内容 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 举报评论 [/comments/{id}/report] [POST]

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