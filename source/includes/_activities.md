# Activities 活动

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的活动对象 ID，16位数字组成的字符串 |
**url** | Sring | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 活动的名称 |
**slug** | String | 活动标识符 |
**city** | String | 活动举办城市 |
**startDate** | String | 活动起始日期 |
**endDate** | String | 活动截止日期 |
**signStartDate** | String | 活动报名起始日期 |
**signEndDate** | String | 活动报名截止日期 |
**bannerUrl** | String | banner的 url |
**address** | String | 活动举办地址 |
**excerpt** | String | 纯文本格式的活动简介 |
**signUrl** | String | 原报名链接 |
**parsedText** | String | 解析为 HTML 后的活动正文 |
**signs** | Int | 已报名人数 |
**isJoin** | Bool | 表示用户是否报名此活动 |
**isSignEnd** | Bool | 是否报名结束 |
**isEnd** | Bool | 活动是否结束 |
**isThirdPartyJoin** | Bool | 是否来自三方 |
**tags** | Array | 活动举办的标签，由一个或多个标签组成 |
**joinedUsers** | Array | 已报名的用户 |
**sponsors** | Array | 赞助商列表，活动将由一个或多个单位赞助 |
**hosts** | Array | 举办方列表，活动将由一个或多个单位举办发起 |

## 活动列表 [/activities] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1160000008640894",
		"url": "/e/1160000008640894",
		"name": "移动互联数据创新",
		"slug": "yidong115504",
		"signs": "0",
		"city": "深圳",
		"hosts": [],
		"sponsors": [
		  "个推",
		  ...
		],
		"bannerUrl": "https://sfault-activity.b0.upaiyun.com/394/778/3947783015-58c216131d63f_big",
		"startDate": "2017-03-26 09:00",
		"endDate": "2017-03-26 18:00",
		"excerpt": "活动简介： 移动互联网推动着场景的裂变，消费的升级以及数据的变革。全球的资源正在被全面打通，未来的价值颠覆我们想象。2017，创新之都，岭南际会。这场由大数据推送技术服务商“个推”主办的千人大会将对话众多...",
		"categoryName": "线下活动",
		"tags": [
		  {
			"name": "数据",
			"url": "/t/%E6%95%B0%E6%8D%AE",
			"id": "1040000000441863",
			"iconUrl": ""
		  },
		  ...
		]
	  },
	  ...
	]
  }
}
```

根据指定 `type` 返回一个 `Activity` 对象的列表。列表总是按照创建时间进行排序，总是将最近的 `Activity` 对象显示在最前面。

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 问题列表类型，共 2 种，`recommend`：推荐，`all`：全部 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 活动详情 [/activities/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1160000008640894",
	"url": "/e/1160000008640894",
	"name": "移动互联数据创新",
	"slug": "yidong115504",
	"city": "深圳",
	"sponsors": [
	  "个推",
	  ...
	],
	"signs": "0",
	"hosts": [],
	"address": "大中华喜来登酒店六楼",
	"bannerUrl": "https://sfault-activity.b0.upaiyun.com/394/778/3947783015-58c216131d63f_medium",
	"isSignEnd": false
	"isEnd": false,
	"isJoined": false,
	"startDate": "2017-03-26 09:00",
	"endDate": "2017-03-26 18:00",
	"signStartDate": "1970-01-01 08:00",
	"signEndDate": "2017-03-26 09:00",
	"excerpt": 
	  "活动简介： 移动互联网推动着场景的裂变，消费的升级以及数据的变革。全球的资源正在被全面打通，未来的价值颠覆我们想象。2017，创新之都，岭南际会。这场由大数据推送技术服务商“个推”主办的千人大会将对话众多...",
	"parsedText": "\n<h2>活动简介：</h2>...",
	"joinedUsers": [],
	"isThirdPartyJoin": true,
	"signUrl": "http://www.getui.com/cn/2017summit.html",
	"tags": [
	  {
		"name": "数据",
		"url": "/t/%E6%95%B0%E6%8D%AE",
		"id": "1040000000441863",
		"iconUrl": ""
	  }
	]
  }
}
```

## 报名活动 [/activities/{id}/join] [POST]

## 活动评论列表 [/activities/{id}/comments] [GET]


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

## 评论活动 [/activities/{id}/comments] [POST]

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

## 删除评论 [/activities/{id}/comments] [DELETE]

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


