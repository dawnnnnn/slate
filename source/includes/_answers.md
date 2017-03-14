# Answers 答案
你可以创建一个 `Answer` 对象对用户提出的答案进行作答。`Answer`是个答案对象，所有答案的主要信息都存储在这个对象中，可以通过发起回答请求来创建一个新的 `Answer` 对象，一个 `Question`对象可以关联多个 `Answer` 对象。每个 `Question` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的答案对象 ID，16位数字组成的字符串 |
**currentStatus** | String | 答案当前状态，共有 3 种 (`available` 可用的，`ignored` 被折叠，`accepted` 已采纳)|
**created** | Timestamp | 答案创建时间的 Unix 时间戳 |
**createdDate** | String | 根据 `created` 解析的时间 |
**likes** | Int | 该答案的认可数，结果 = 用户赞同数 - 用户反对数 |
**comments** | Int | 该答案的评论数，结果 = 评论答案数 + 回复评论数 |
**isAccepted** | Bool | 表示该答案是否已被题主采纳为最佳答案 |
**isIgnored** | Bool | 表示该答案是否已被用户忽略 |
**isLiked** | Bool | 表示查看该答案的用户是否赞同该答案，未登录查看默认状态为 `false` |
**isHated** | Bool | 表示查看该答案的用户是否反对该答案，未登录查看默认状态为 `false` |
**canEdit** | Bool | 表示查看该答案的用户是否能编辑该答案，未登录查看默认状态为 `false` |
**excerpt** | String | 答案的摘录，将除文字外的特殊片段转为文字描述，如{代码...} |
**originalText** | String | 答案主体部分的原文，即题主提问时撰写的原文 |
**parsedText** | String | 解析为 HTML 后的答案主体部分 |
**user** | Object | 创建该答案的用户对象 |

## 问题答案列表 [/questions/{id}/answers] [GET]

> 示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1020000008635960",
		"url": "/q/1010000008635436/a-1020000008635960",
		"currentStatus": "available",
		"likes": "3",
		"comments": "1",
		"isLiked": false,
		"isHated": false,
		"isIgnore": false,
		"isAccepted": false,
		"isEdited": true,
		"isAuthor": false,
		"createdDate": "18 小时前",
		"modifiedDate": "18 小时前",
		"originalText": 
		  "```\n/function\\s+([^\\s(]*)/\n```\n\n\n```\n\\s = 空白，对应上边的空格\n[^\\s] = [^空白] = 不是空白\n+ 一次或多次匹配\n* 任意次匹配（包含0次）\n```\n\n```\n表达式的［( /function\\s+([^\\s(]*)/ )］匹配项：\"function myFn\"  \n\n［([^\\s(]*)］中的分组1对应的匹配项［不为空，不能是( ］：\"myFn\"\n```\n\n",
		"parsedText": 
		  "\n<pre><code>/function\\s+([^\\s(]*)/</code></pre>\n<pre><code>\\s = 空白，对应上边的空格\n[^\\s] = [^空白] = 不是空白\n+ 一次或多次匹配\n* 任意次匹配（包含0次）</code></pre>\n<pre><code>表达式的［( /function\\s+([^\\s(]*)/ )］匹配项：\"function myFn\"  \n\n［([^\\s(]*)］中的分组1对应的匹配项［不为空，不能是( ］：\"myFn\"</code></pre>\n",
	  },
	  ...
	]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `Question` 问题对象的 id |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 回答问题 [/questions/{id}/answers] [POST]

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1020000008635960",
	"url": "/q/1010000008635436/a-1020000008635960",
	"currentStatus": "available",
	"likes": "0",
	"comments": "0",
	"isLiked": false,
	"isHated": false,
	"isIgnore": false,
	"isAccepted": false,
	"isEdited": true,
	"isAuthor": false,
	"createdDate": "18 小时前",
	"modifiedDate": "18 小时前",
	"originalText": 
	  "```\n/function\\s+([^\\s(]*)/\n```\n\n\n```\n\\s = 空白，对应上边的空格\n[^\\s] = [^空白] = 不是空白\n+ 一次或多次匹配\n* 任意次匹配（包含0次）\n```\n\n```\n表达式的［( /function\\s+([^\\s(]*)/ )］匹配项：\"function myFn\"  \n\n［([^\\s(]*)］中的分组1对应的匹配项［不为空，不能是( ］：\"myFn\"\n```\n\n",
	"parsedText": 
	  "\n<pre><code>/function\\s+([^\\s(]*)/</code></pre>\n<pre><code>\\s = 空白，对应上边的空格\n[^\\s] = [^空白] = 不是空白\n+ 一次或多次匹配\n* 任意次匹配（包含0次）</code></pre>\n<pre><code>表达式的［( /function\\s+([^\\s(]*)/ )］匹配项：\"function myFn\"  \n\n［([^\\s(]*)］中的分组1对应的匹配项［不为空，不能是( ］：\"myFn\"</code></pre>\n",
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `Question` 问题对象的 id |
**text** | String | 用户撰写的答案正文，限制字数 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改答案 [/questions/{id}/answers] [PUT]

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `Question` 问题对象的 id |
**answerId** | String | 在 parameter 中带上需要修改的 `Answer` 对象 id |
**text** | String | 修改后的答案正文，限制字数 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除答案 [/questions/{id}/answers] [DELETE]

> 示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `Question` 问题对象的 id |
**answerId** | String | 在 parameter 中带上需要删除的 `Answer` 对象 id |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 答案评论列表 [/answers/{id}/comments] [GET]

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
		"repliedCommentCount": "2",
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
**repliedCommentCount** | Int | 该评论的回复数 |
**repliedComments** | Array | 该评论的回复列表，最多返回 3 项，如有超过 3 项回复，需另外发起请求 |
**isLiked** | Bool | 表示查看该评论的用户是否为该评论点赞，未登录查看默认状态为 `false` |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 发布答案评论 [/answers/{id}/comments] [POST]

发起创建 `Comment` 对象的请求，需要对用户验证是否为登录状态。

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": 1050000008644845,
	"likes": "0",
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
	"repliedCommentCount": "0",
	"repliedComments": []
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**text** | String | 评论的内容，限制长度? |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除评论 [answers/{id}/comments] [DELETE]

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 赞同答案 [/answers/{id}/likes] [POST]

当前用户对该答案为 `已反对` 状态时，发送该请求时，默认用户对该答案 `取消反对` 并 `赞同` 的操作。

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消赞同答案 [/answers/{id}/likes] [DELETE]

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 反对答案 [/answers/{id}/hates] [POST]

当前用户对该答案为 `已赞同` 状态时，发送该请求时，默认用户对该答案 `取消赞同` 并 `反对` 的操作。

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消反对答案 [/answers/{id}/hates] [DELETE]

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 举报答案 [/answers/{id}/report] [POST]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**reason** | String | 举报问题的原因，共 4 种 （`垃圾信息`, `违规内容`, `不友善内容`, `内容质量差`） |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>







