# Favotites 收藏

你可以创建一个 `Favorite` 对象用作归档自己对其他资源的集合。`Favorite`是个收藏夹对象，可以通过发起创建收藏夹请求来创建一个新的 `Favorite` 对象，也可以随时查询其他用户或自己的 `Favorite` 对象的信息。每个 `Favorite` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的收藏夹对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 收藏夹的名称，简洁概括 |
**desc** | String | 收藏夹的描述，可进一步介绍创建该收藏夹的缘由 |
**entriesCount** | Int | 收藏夹条目数量 |
**followers** | Int | 收藏夹的关注者数量 |
**isFollowed** | Bool | 是否关注这个收藏夹 |
**isPrivated** | Bool | 是否为私有的收藏夹，即仅对自己可见 |
**isAuthor** | Bool | 作者是否为自己 |
**user** | Object | 创建收藏夹的用户 |
**entries** | Array | 收藏夹夹下的所有条目 |

## 创建收藏夹 [/favorites] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1230000007550478",
	"url": "/favorite/1230000007550478",
	"name": "asdad",
	"desc": "dasda",
	"entriesCount": "0",
	"followers": "0",
	"isFollowed": false,
	"isPrivate": true,
	"isAuthor": true,
    "user": {
	  "id": "1030000004958804",
	  "name": "testoopser",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_huge128",
	  "url": "/u/testoopser"
    },
    "entries": []
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String | 创建收藏夹时填写的收藏夹名称，限制长度 |
**desc** | String | 创建收藏夹时填写的收藏夹描述 |
**isPrivate** | Bool | 是否设置为仅自己可见的收藏夹 |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 更新收藏夹 [/favorites] [PUT]

> 示例参照创建收藏夹

请求参数 | | |
-------------- | -------------- | -------------- |
**favoriteId** | 由 SegmentFault 生成的收藏夹对象 ID，16位数字组成的字符串 | 
**name** | String | 创建收藏夹时填写的收藏夹名称，限制长度 |
**desc** | String | 创建收藏夹时填写的收藏夹描述 |
**isPrivate** | Bool | 是否设置为仅自己可见的收藏夹 |

<aside class="notice">
只有登录用户且为收藏夹的创建者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除收藏夹 [/favorites] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

属性 | | |
-------------- | -------------- | -------------- |
**favoriteId** | 由 SegmentFault 生成的收藏夹对象 ID，16位数字组成的字符串 | 

<aside class="notice">
只有登录用户且为收藏夹的创建者可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 收藏夹信息 [/favorites/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1230000007550478",
	"url": "/favorite/1230000007550478",
	"name": "asdad",
	"desc": "dasda",
	"entriesCount": "0",
	"followers": "0",
	"isFollowed": false,
	"isPrivate": "1",
	"isAuthor": true,
    "user": {
	  "id": "1030000004958804",
	  "name": "testoopser",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_huge128",
	  "url": "/u/testoopser"
    },
    "entries": [
      {
		"id": "1210000008652727",
		"url": "/p/1210000008652727",
		"title": "代码神注释，让我们认真对待一次",
		"createdDate": "5 天前",
		"likes": "10",
		"favorites": "34",
		"type": "url",
		"user": {
		  "id": "1030000008431166",
		  "name": "清蒸不是水煮",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/375/587/3755876833-58ad20efd15b6_big64",
		  "url": "/u/e_vae_va_z"
		},
		"tags": []
	  },
	  {
		"id": "1190000004976815",
		"url": "/a/1190000004976815",
		"title": "[译] LLDB 基础",
		"type": "article",
		"likes": "3",
		"createdDate": "2016年04月20日",
		"comments": "2",
		"excerpt": "原文链接：https://swifting.io/blog/2016/02/19/6-basic-lld...",
		"bookmarks": 17,
		"blog": {
		  "name": "wamaker @ segmentfault",
		  "url": "/blog/wamaker"
		},
		"user": {
		  "id": "1030000004606368",
		  "name": "WAMake",
		  "rank": "316",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/171/025/1710252095-5885766df1ab1_small",
		  "url": "/u/wamaker"
		},
		"tags": [
		  {
			"name": "iOS",
			"id": "1040000000089442",
			"url": "/t/iOS"
		  },
		  {
			"name": "lldb",
			"id": "1040000000619566",
			"url": "/t/lldb"
		  }
		]
	  }
    ]
  }
}
```

`entries` 返回的内容为各种类型的集合，现对 `entries` 列表内对象作如下说明
 
返回说明 | | |
-------------- | -------------- | -------------- |
**type** | String | 收藏条目的类型，共 5 种 (`article`：文章， `question`：问题，`url`：链接头条，`note`：笔记，`text`：文本头条 ) |
**id** | String | 收藏夹内条目的 id |
**url** | String | 收藏夹内条目的 url |
**title** | String | 收藏夹内条目的 标题 |
**createdDate** | String | 收藏夹内条目的 创建日期 |
**likes** | Int | 收藏夹内条目的 被赞数目 |
**favorites** | Int | 收藏夹内条目的 被收藏数目 |
**comments** | Int | 收藏夹内条目的 评论数目 |
**answers** | Int | type 为 `question` 问题对象时，表示答案数目 |
**isAccepted** | Bool | type 为 `question` 问题对象时, 表示是否已采纳答案，其余返回为 `false` |
**user** | Object | 收藏夹内条目的创建者 用户对象 |
**blog** | Object | type 为 `article`文章对象时，文章所属的专栏对象，type不为`article`时，返回空 |
**tags** | Array | 条目所属的标签, 由一个或多个组成，type 为 `url` 或 `text` 时返回空|

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 关注收藏夹 [/favorites/{id}/follows] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": true
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消关注收藏夹 [/favorites/{id}/follows] [DELETE]

> 返回示例 

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": false
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>