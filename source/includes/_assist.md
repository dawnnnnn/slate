# Assist 辅助接口

## 全局搜索 [/search] [GET]

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 用户的搜索关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 搜索学校 [schools/search] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
		"id": "1310000003080744",
		"name": "浙江大学",
		"slug": "zhejiangdaxue",
		"stateName": "浙江"
	  },
	  {
		"id": "1310000003080745",
		"name": "浙江理工大学",
		"slug": "zhejiangligongdaxue",
		"stateName": "浙江"
	  },
	  ...
    ]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 用户的搜索关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 排行 [/ranks] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
  	"rows": [
	  {
		"id": "1030000005127735",
		"ranks": "152",
		"avatarUrl": "https://sfault-avatar.b0.upaiyun.com/364/787/3647877757-58c236fe63c80_big64",
		"name": "realwate",
		"url": "/u/realwate",
		"increase": "66",
		"slug": "realwate"
	  },
      {
        "id": "1030000002698293",
        "ranks": "9.6k",
        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/320/008/3200081217-57c6b8e5a4372_big64",
        "name": "zonxin",
        "url": "/u/zonxin",
        "increase": "62",
        "slug": "zonxin"
      },
      ...
  	]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 共 5 种 （`annual`：年度，`quarter`：季度，`monthly`：月度，，`weekly`：周度，`daily`：日常） |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 消息推送设置列表 [/settings/notifications] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"answerPush": false,
	"followPush": false,
	"likePush": false,
	"messagePush": true,
	"commentPush": true,
	"mentionPush": true,
	"invitePush": true,
	"disturb": true
  }
}
```

## 消息推送设置 [/settings/notifications] [PATCH]

> 返回示例 参照消息推送设置列表

请求参数 | | |
-------------- | -------------- | -------------- |
**answerPush** | Bool | 关注的问题有了新答案时，是否推送 |
**followPush** | Bool | 有人关注我时，是否推送 |
**likePush** | Bool | 有人给我投票，是否推送 |
**messagePush** | Bool | 有人给我私信，是否推送 |
**commentPush** | Bool | 有人评论我，是否推送 |
**mentionPush** | Bool | 有人提到我，是否推送 |
**invitePush** | Bool | 有人邀请我回答问题，是否推送 |
**disturb** | Bool | 是否开启 勿扰模式 |

## 三方绑定列表 [/settings/oauths] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"google": true,
	"weibo": false,
	"qq": false,
	"wechat": false,
	"github": true
  }
}
```

## 绑定第三方 [/settings/oauths] [POST]

``` json
{
  "status": 0,
  "message": "",
  "data": {
  	"qq": {
	  "id": "008E0EAE7ECAE76DFEAA34B29A98656C",
	  "is_hide": "0",
	  "name": "\U817e\U8baf QQ",
	  "token": "s:32:\"AC1A768BC9401F6190FD1306472AC5FA\";",
	  "type": "qq",
	  "url": "",
	  "user_id": "1030000004603175"
	}
  }
}

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 第三方绑定的类型，共 5 种 (`wechat`: 微信，`qq`: 腾讯 QQ, `weibo`: 新浪微博, `github`: Github, `google`: Google) |
**accessToken** | String | 三方传回的 token |
**unionId** | String | 三方传回的 union id |

## 三方显示列表 [/settings/oauths/show] [GET]

> 返回示例 

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"weibo": false,
	"google": false,
	"github": false,
	"wechat": false,
	"qq": false
  }
}
```

## 三方显示列表设置 [/settings/oauths/show] [PATCH]

> 返回示例 三方显示列表

请求参数 | | |
-------------- | -------------- | -------------- |
**weibo** | Bool | 是否显示微博 |
**google** | Bool | 是否显示google |
**github** | Bool | 是否显示Github |
**wechat** | Bool | 是否显示微信 |
**qq** | Bool | 是否显示腾讯QQ |

## 私信聊天记录 [/messages/{userId}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1440000007957551",
		"content": "2222",
		"created": "1482992731",
		"createdDate": "2016年12月29日",
		"isSystem": 0,
		"userId": "1030000004603175"
	  },
	  {
		"id": "1440000007954635",
		"content": "23333",
		"created": "1482979699",
		"createdDate": "2016年12月29日",
		"isSystem": 0,
		"userId": "1030000004603175"
	  },
	  ...
	]
  }
}
```

## 发送私信 [/message/{userId}] [POST]

> 返回示例 

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1440000007954635",
	"content": "23333",
	"created": "1482979699",
	"createdDate": "2016年12月29日",
	"isSystem": 0,
	"userId": "1030000004603175"
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**content** | String | 私信发送的纯文本内容 |
