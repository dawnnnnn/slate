# Tags 标签

`Tag`是个标签对象，所有标签的主要信息都存储在这个对象中，可以通过发起创建标签请求来创建一个新的 `Tag` 对象，也可以随时查询一个或多个 `Tag` 对象的信息。每个 `Tag` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 标签的名称 |
**shortUrl** | String | 标签的短链接 |
**excerpt** | String | 标签的摘要 |
**parsedText** | String | 标签的描述解析 |
**orginalText** | String | 标签的描述原文 |
**thumbnailUrl** | String | 标签的默认图片 url |
**followers** | Int | 标签的关注者数量 |
**isFollowed** | Bool | 查看该标签的用户，是否已关注此标签 |

## 标签列表 [/tags] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1040000000089436",
		"url": "/t/javascript",
    	"name": "javascript"
	  },
	  {
		"id": "1040000000089423",
		"url": "/t/python",
    	"name": "python"
	  },
	  ...
	]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 获取 `tag` 列表的类型，共种 （`hottest`：热门的，`all`：全部的，`followed`：已关注的） |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

<aside class="notice">
当前为登录用户状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 创建标签 [/tags] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1040000000089436",
    "url": "/t/javascript",
    "name": "javascript",
    "parsedText": 
      "\n<p>JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。</p>\n<p>一般来说，完整的JavaScript包括以下几个部分：</p>\n<ul>\n<li><p>ECMAScript，描述了该语言的语法和基本对象</p></li>\n<li><p>文档对象模型（DOM），描述处理网页内容的方法和接口</p></li>\n<li><p>...",
    "originalText": 
      "JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。\n\n一般来说，完整的JavaScript包括以下几个部分：\n- ECMAScript，描述了该语言的语法和基本对象\n- 文档对象模型（DOM），描述处理网页内容的方法和接口\n- ...",
    "excerpt": 
      "JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。 一般来说，完整的JavaScript包括以下几个部分： ECMAScript，描述了该语言的语法和基本对象 文档对...",
    "followers": "0",
    "isFollowed": false,
    "thumbnailUrl": "https://sfault-avatar.b0.upaiyun.com/195/823/1958237468-1040000000089436_small"
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String | 创建的标签名 |
**desc** | String | 标签的描述 |

<aside class="notice">
只有登录用户才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改标签 [/tags] [PUT]

> 返回示例参照标签详情

请求参数 | | |
-------------- | -------------- | -------------- |
**tagId** | String | 由 SegmentFault 生成的标签对象 ID，16位数字组成的字符串 |
**name** | String | 创建的标签名 |
**desc** | String | 标签的描述 |

<aside class="notice">
只有登录用户才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除标签 [/tags] [DELETE]

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
**tagId** | String | 由 SegmentFault 生成的标签对象 ID，16位数字组成的字符串 |

<aside class="notice">
只有登录用户才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 标签详情 [/tags/{id}] [GET]

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"id": "1040000000089436",
    "url": "/t/javascript",
    "name": "javascript",
    "parsedText": 
      "\n<p>JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。</p>\n<p>一般来说，完整的JavaScript包括以下几个部分：</p>\n<ul>\n<li><p>ECMAScript，描述了该语言的语法和基本对象</p></li>\n<li><p>文档对象模型（DOM），描述处理网页内容的方法和接口</p></li>\n<li><p>...",
    "originalText": 
      "JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。\n\n一般来说，完整的JavaScript包括以下几个部分：\n- ECMAScript，描述了该语言的语法和基本对象\n- 文档对象模型（DOM），描述处理网页内容的方法和接口\n- ...",
    "excerpt": 
      "JavaScript 是一门弱类型的动态脚本语言，支持多种编程范式，包括面向对象和函数式编程，被广泛用于 web 开发。 一般来说，完整的JavaScript包括以下几个部分： ECMAScript，描述了该语言的语法和基本对象 文档对...",
    "followers": "18263",
    "isFollowed": true,
    "thumbnailUrl": "https://sfault-avatar.b0.upaiyun.com/195/823/1958237468-1040000000089436_small"
  }
}
```

<aside class="notice">
当前为登录用户状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 标签下的用户排行 [/tags/{id}/ranks] [GET]

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1030000000747771",
		"url": "/u/hampotato",
		"name": "戴仓薯",
		"avatarUrl": "https://sfault-avatar.b0.upaiyun.com/365/043/365043127-54a91b4394c06_small",
		"increase": "4554",
		"slug": "hampotato"
	  },
	  {
		"id": "1030000000093502",
		"url": "/u/openfibers",
		"name": "OpenFibers",
		"avatarUrl": "https://sfault-avatar.b0.upaiyun.com/384/738/3847382589-1030000000093502_small",
		"increase": "2201",
		"slug": "openfibers"
	  },
	  ...
	]
  }
}
```

返回说明 | | |
-------------- | -------------- | -------------- |
**increase** | Int | 用户在该标签下所获得的声望值 |

## 标签搜索 [/tags/search] [GET]

> 返回示例参照标签列表

根据提供的关键词，搜索标题或内容中带有该关键词的标签，返回一个 `Tag` 对象的列表。

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 搜索的关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

## 关注标签 [/tags/{id}/follows] [POST]

> 返回示例

{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": true
  }
}

<aside class="notice">
只有登录用户才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消关注标签 [/tags/{id}/follows] [DELETE]

> 返回示例

{
  "status": 0,
  "message": "",
  "data": {
	"isFollowed": false
  }
}

<aside class="notice">
只有登录用户才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>
