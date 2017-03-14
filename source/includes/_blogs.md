# Blogs 专栏

你可以创建一个 `Blog` 对象来归档自己的文章。在写文章前必须先拥有一个专栏，你可以通过发起创建文章请求来创建一个新的 `Blog` 对象。每个 `Blog` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的专栏对象 id，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，后缀由创建用户创建专栏对象时自定义slug |
**name** | String | 专栏的名称 |
**desc** | String | 专栏的简介，简单概括开专栏的原因或专栏的主要主题，限制长度 |
**currentStatus** | String ||
**isFollowed** | Bool | 表示查看该专栏的用户是否关注了该问题，未登录查看默认状态为 `false` |
**articles** | Int | 该专栏下，已发布文章的数量 |
**followers** | Int | 关注该专栏的用户数量 |
**user** | Object | 创建该专栏的用户对象 |
**Authors** | Array | 该专栏下的所有作者 |

## 专栏列表 [/user/{id}/blogs] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1200000000366002",
		"url": "/blog/gemini"
		"name": "Gemini's blog",
		"desc": "Gemini @ SegmentFault",
		"currentStatus": "available",
		"isFollowed": false,
		"followers": "34",
		"user": {
		  "id": "1030000000199113",
		  "url": "/u/gemini",
		  "name": "Gemini",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/345/679/3456790589-575d08ad437b0_medium40",
		}
	  },
	  ...
	]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `User` 用户对象的 id |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

<aside class="notice">
登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 创建专栏 [/user/{id}/blogs] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1200000000366002",
	"url": "/blog/gemini"
	"name": "Gemini's blog",
	"desc": "Gemini @ SegmentFault",
	"currentStatus": "available",
	"isFollowed": false,
	"followers": "0",
	"user": {
	  "id": "1030000000199113",
	  "url": "/u/gemini",
	  "name": "Gemini",
	  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/345/679/3456790589-575d08ad437b0_medium40",
	},
	"Authors": []
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `User` 用户对象的 id |
**name** | String | 创建专栏时所取的专栏名称 |
**desc** | String | 创建专栏时简单概括的专栏简介 |
**slug** | String | 自定义专栏后缀，例: segmentfault.com/blog/slug |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改专栏 [/user/{id}/blogs] [PUT]

> 返回示例参照创建专栏

请求参数 | | |
-------------- | -------------- | -------------- |
**id** | String | url 中所带 id 为 `User` 用户对象的 id |
**blogId** | String | `Blog` 专栏对象的唯一标识 |
**name** | String | 创建专栏时所取的专栏名称 |
**desc** | String | 创建专栏时简单概括的专栏简介 |
**slug** | String | 自定义专栏后缀，例: segmentfault.com/blog/slug |
**userSlugs** | Array | 添加一个或多个用户为专栏的作者，提供用户的 `slug` |

<aside class="notice">
只有登录用户并且为专栏创建者才可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除专栏 [user/{id}/blogs] [DELETE]

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
**id** | String | url 中所带 id 为 `User` 用户对象的 id |
**blogId** | String | `Blog` 专栏对象的唯一标识 |

<aside class="notice">
只有登录用户并且为专栏创建者才可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 专栏信息 [/blogs/{id}] [GET]

> 返回示例参照创建专栏

<aside class="notice">
登录状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 专栏文章 [/blogs/{id}/articles] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1190000008437202",
		"url": "/a/1190000008437202",
		"title": "Java NIO 入门",
		"likes": "0",
		"comments": "0",
		"favorites": "0",
		"createdDate": "2月22日",
		"excerpt": 
		  "关于多路复用 很多人用过InputStream和OutputStream接口，用来操作文件、Socket等等 IO 操作。如果是简单的，速度较快的 IO 操作，我们用Stream类的接口，依然可以风生水起。如果你要使用非阻塞的 IO 的话，他们...",
		"blog": {
		  "id": "1200000000366002",
		  "name": "Gemini @ SegmentFault",
		  "desc": "Gemini's blog",
		  "url": "/blog/gemini"
		},
		"user": {
		  "id": "1030000000199113",
		  "name": "Gemini",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/345/679/3456790589-575d08ad437b0_small",
		  "url": "/u/gemini"
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

## 关注专栏 [/blogs/{id}/follows] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": true,
	"follower": "3"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消关注专栏 [/blogs/{id}/follows] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": false,
	"follower": "2"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

