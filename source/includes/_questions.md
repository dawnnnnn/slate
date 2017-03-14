# Questions 问题 
你可以创建一个 `Question` 对象向用户提问。`Question`是个问题对象，所有问题的主要信息都存储在这个对象中，可以通过发起提问请求来创建一个新的 `Question` 对象，也可以随时查询一个或多个 `Question` 对象的信息。每个 `Question` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**title** | String | 问题的标题，一句话简洁概括问题的主要内容 |
**currentStatus** | String | 问题当前状态，共有 5 种 (`available` 可用的，`pending` 审核中，`rejected` 被拒绝，`closed` 已关闭，`deleted` 已删除 )|
**created** | Timestamp | 问题创建时间的 Unix 时间戳 |
**createdDate** | String | 根据 `created` 解析的时间 |
**likes** | Int | 该问题的认可数，结果 = 用户赞同数 - 用户反对数 |
**comments** | Int | 该问题的评论数，结果 = 评论问题数 + 回复评论数 |
**answers** | Int | 该问题的答案数 |
**favorites** | Int | 该问题的收藏数，即多少名用户收藏了该问题 |
**followers** | Int | 该问题的关注数，即多少名用户关注了该问题，关注者在该问题有新回答会收到提示 |
**viewCount** | Int | 该问题的查看次数 |
**isAccepted** | Bool | 表示该问题是否已被题主采纳最佳答案 |
**isClosed** | Bool | 表示该问题是否被题主或管理员关闭 |
**isLiked** | Bool | 表示查看该问题的用户是否赞同该问题，未登录查看默认状态为 `false` |
**isHated** | Bool | 表示查看该问题的用户是否反对该问题，未登录查看默认状态为 `false` |
**isFollowed** | Bool | 表示查看该问题的用户是否关注了该问题，未登录查看默认状态为 `false` |
**isFavorited** | Bool | 表示查看该问题的用户是否收藏了该问题，未登录查看默认状态为 `false` |
**canEdit** | Bool | 表示查看该问题的用户是否能编辑该问题，未登录查看默认状态为 `false` |
**excerpt** | String | 问题的摘录，将除文字外的特殊片段转为文字描述，如{代码...} |
**originalText** | String | 问题主体部分的原文，即题主提问时撰写的原文 |
**parsedText** | String | 解析为 HTML 后的问题主体部分 |
**user** | Object | 创建该问题的用户对象 |
**tags** | Array | 与该问题相关的 `tag` 对象列表，最多 5 项，均由用户创建问题时提供 |
**answer** | Array | 该问题下所有回答列表 |
**suggestion** | Array | 与该问题相关或相似的问题列表 |


## 问题列表 [/questions] [GET]

> Resopnse示例

```json
{
  "status": 0,
  "message": "",
  "data": {
  	"rows": [
  	  {
  	    "id": "1010000008642492",
  	    "url": "/q/1010000008642492",
  	    "title": "mongoose中的addCreateAt方法作用",
  	    "created": 1489122678,
  	    "createdDate": "3 小时前",
  	    "isAccepted": false,
  	    "isClosed": false,
  	    "likes": "5",
  	    "answers": "7",
  	    "user": {
  		    "id": "1030000007418730",
  		    "name": "FatDong1",
  		    "slug": "fatgong1",
  		    "avatarUrl": "http://sfault-avatar.b0.upaiyun.com/266/885/2668851129-584c1625700ce_medium40",
  		    "url": "/u/fatgong1"
  	    },
  	    "tags": [
          {
            "name": "mongoose",
            "id": "1040000000345321"
  		    },
  		    {
            "name": "mongodb",
            "id": "1040000000089488"
  		    },
          ...
  	    ]
  	  },
      ...
  	]
  }
}
```

根据指定 `type` 返回一个 `Question` 对象的列表。除 `newest` 外，列表总是按照创建时间进行排序，总是将最近的 `Question` 对象显示在最前面。

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 问题列表类型，共4种，`hottest`：最热，`newest`：最新，`unanswered`：未回答的，`tag`：标签 |
**tag** _optional_| String | type 为 `tag` 时必传，填写 tag 的 slug 或者 id |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |


## 提问题 [/questions] [POST]

> 示例参见问题详情

发起创建 `Question` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**title** | String | 问题的标题，限制长度 6-64 个字 |
**tags**  | Array  | 问题的标签，限制个数 1-5 个，|
**text**  | String | 问题的内容，限制长度 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 编辑问题 [/questions] [PUT]

> 示例参见问题详情

发起修改 `Question` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**questionId** | String | 问题的id |
**title** | String | 问题的标题，限制长度 6-64 个字 |
**tags** | Array | 问题的标签，限制个数 1-5 个，|
**text** | String | 问题的内容，限制长度 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除问题 [/questions] [DELETE]

> 示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

发起删除 `Question` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**questionId** | String | 问题的id |

<aside class="notice">
登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>


## 搜索问题 [/questions/search] [GET]

> 示例参见问题列表

根据提供的关键词，搜索标题或内容中带有该关键词的问题，返回一个 `Question` 对象的列表。

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 搜索的关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

## 问题详情 [/questions/{id}] [GET]

> 示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1010000008635436",
    "url": "/q/1010000008635436",
    "title": "preg_match的理解",
    "currentStatus": "available",
    "created": "1489070208",
    "createdDate": "19 小时前",
    "likes": "0",
    "comments": "2",
    "answers": "4",
    "favorites": 0,
    "followers": 7,
    "viewCount": 123,
    "isAccepted": false,
    "isClosed": false,
    "isLiked": false,
    "isHated": false,
    "isFollowed": false,
    "isFavorited": false,
    "canEdit": true,
    "excerpt": 
      "无法理解后半段话 举例： {代码...} 对着文档，看着例子，还是无法理解，myFn是怎么出来的。正则本身就是来找function xxx这样的字符串的，为什么就把myFn找出来了？",
    "originalText": 
      "无法理解后半段话\n\n![clipboard.png](/img/bVKoCP)\n\n举例：\n    $str=\"public function myFn (a, b){//...}\";\n    preg_match('/function\\s+([^\\s(]*)/',$str,$m);\n    var_dump($m);\n    // 输出\n    array(2) {\n      [0]=>\n      string(13) \"function myFn\"\n      [1]=>\n      string(4) \"myFn\"\n    }\n对着文档，看着例子，还是无法理解，myFn是怎么出来的。正则本身就是来找function xxx这样的字符串的，为什么就把myFn找出来了？",
    "parsedText": 
      "<html><body>\n<p>无法理解后半段话</p>\n<p><img src=\"/img/bVKoCP?w=675&amp;h=281\" alt=\"clipboard.png\" title=\"clipboard.png\"></p>\n<p>举例：</p>\n<pre><code>$str=\"public function myFn (a, b){//...}\";\npreg_match('/function\\s+([^\\s(]*)/',$str,$m);\nvar_dump($m);\n// 输出\narray(2) {\n  [0]=&gt;\n  string(13) \"function myFn\"\n  [1]=&gt;\n  string(4) \"myFn\"\n}</code></pre>\n<p>对着文档，看着例子，还是无法理解，myFn是怎么出来的。正则本身就是来找function xxx这样的字符串的，为什么就把myFn找出来了？</p>\n</body></html>",
	"tags": [
      {
        "name": "php",
        "url": "/t/php",
        "id": "1040000000089387"
      },
      ...
    ],
    "user": {
      "id": "1030000004461013",
      "name": "waker",
      "avatarUrl": "http://static.segmentfault.com/global/img/user-40.png",
      "url": "/u/waker",
      "slug": "waker"
    },
    "answer": [
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
	],
	"suggestion": [
	  {
        "id": "1010000000094629",
        "url": "/q/1010000000094629",
        "title": "php preg_match_all 处理中文的时候出现乱码",
        "answers": "2",
        "isAccepted": false
      },
      {
        "id": "1010000008181451",
        "url": "/q/1010000008181451",
        "title": "php如何判断站内跟站外链接",
        "answers": "1",
        "isAccepted": false
      },
      ...
	]
  }
}
```

发起一个查询问题的请求，返回一个 `Question` 对象的所有属性。

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>


## 相似问题列表 [/questions/{id}/suggestions] [GET]

> 示例

``` json
{
  "status": 0,
  "message" = "",
  "data": {
  	"rows": [
  	  {
        "id": "1010000000094629",
        "url": "/q/1010000000094629",
        "title": "php preg_match_all 处理中文的时候出现乱码",
        "answers": "2",
        "isAccepted": false
      },
      {
        "id": "1010000008181451",
        "url": "/q/1010000008181451",
        "title": "php如何判断站内跟站外链接",
        "answers": "1",
        "isAccepted": false
      },
      ...
  	]
  }
}
```

根据一个 `Question` 对象的 `id` 返回与其相似或相关的问题列表。

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |


## 问题评论列表 [/questions/{id}/comments] [GET]

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

## 发布问题评论 [/questions/{id}/comments] [POST]

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

发起创建 `Comment` 对象的请求，需要对用户验证是否为登录状态。

请求参数 | | |
-------------- | -------------- | -------------- |
**text** | String | 评论的内容，限制长度? |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 邀请回答 [/questions/{id}/invitations] [POST]

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
**slug** | String | 被邀请用户的 `slug`，`slug` 为用户的唯一标识符，一次只可邀请一位用户回答 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 收藏问题 [/questions/{id}/favorites] [POST]

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

## 关注问题 [/questions/{id}/follows] [POST]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFollowed": true,
    "followers": "3"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消关注问题 [/questions/{id}/follows] [DELETE]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFollowed": false,
    "followers": "2"
  }
}
```


<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 赞同问题 [/questions/{id}/likes] [POST]

当前用户对该问题为 `已反对` 状态时，发送该请求时，默认用户对该问题 `取消反对` 并 `赞同` 的操作。

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": true,
    "isHated": false,
    "likes": "3"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消赞同问题 [/questions/{id}/likes] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": false,
    "isHated": false,
    "likes": "2"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 反对问题 [/questions/{id}/hates] [POST]

当前用户对该问题为 `已赞同` 状态时，发送该请求时，默认用户对该问题 `取消赞同` 并 `反对` 的操作。

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": false,
    "isHated": true,
    "likes": "1"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消反对问题 [/questions/{id}/hates] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isLiked": false,
    "isHated": false,
    "likes": "2"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 举报问题 [/question/{id}/report] [POST]

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




