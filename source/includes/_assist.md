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

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 共 4 种 （`monthly`：月度 `annual`：年度 `weekly`：周度 `quarter`：季度） |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 通知 [/settings/notifications] [GET]

## 通知 [/settings/notifications] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**allows** | Array |  |

## 三方绑定列表 [/settings/oauths] [GET]

## 绑定第三方 [/settings/oauths] [POST]

## 三方显示列表 [/settings/oauths/show] [GET]

## 私信聊天记录 [/messages/{userId}] [GET]

## 发送私信 [/message/{userId}] [POST]
