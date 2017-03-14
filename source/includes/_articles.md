# Articles 文章

你可以创建一个 `Article` 对象来记录自己的技术见解和学习收获。`Article`是个文章对象，所有文章的主要信息都存储在这个对象中，可以通过发起创建文章请求来创建一个新的 `Article` 对象，也可以随时查询一个或多个 `Article` 对象的信息。每个 `Article` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的文章对象 id，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**title** | String | 文章的标题，一句话简洁概括文章的主要内容 |
**currentStatus** | String | 文章当前状态，共有 5 种 (`available` 可用的，`pending` 审核中，`rejected` 被拒绝，`deleted` 已删除，`recommend` 被推荐的 )|
**createdDate** | String | 根据 `created` 解析的时间 |
**originalText** | String | 文章主体部分的原文，即作者撰写的原文 |
**parsedText** | String | 解析为 HTML 后的文章主体部分 |
**likes** | Int | 该文章的认可数，结果 = 用户赞同数 - 用户反对数 |
**favorites** | Int | 该文章的收藏数，即多少名用户收藏了该文章 |
**comments** | Int | 该文章的评论数，结果 = 评论文章数 + 回复评论数 |
**viewCount** | Int | 该文章的查看次数 |
**isLiked** | Bool | 表示查看该文章的用户为该文章点赞，未登录查看默认状态为 `false` |
**isAuthor** | Bool | 是否为该文章的作者 |
**isRecommend** | Bool | 表示该文章是否被管理员推荐 |
**isFavorited** | Bool | 表示查看该文章的用户是否收藏了该文章，未登录查看默认状态为 `false` |
**isDelete** | Bool | 表示该文章是否被作者或管理员删除 |
**isShowLicense** | Bool | 表示该文章是否 |
**canEdit** | Bool | 表示查看该文章的用户是否能编辑该文章，未登录查看默认状态为 `false` |
**excerpt** | String | 文章的摘录，将除文字外的特殊片段转为文字描述，如{代码...} |
**user** | Object | 创建该文章的用户对象 |
**blog** | Object | 该文章所属的专栏对象 |
**tags** | Array | 与该文章相关的 `tag` 对象列表，最多 5 项，均由用户创建文章时提供 |
**commentsDetail** | Array | 该文章下部分评论列表 |
**suggestions** | Array | 与该文章相关或相似的问题列表 |

## 文章列表 [/articles] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"id": "1190000008686643",
		"url": "/a/1190000008686643",
    	"title": "WebAssembly 工作原理",
    	"likes": "0",
    	"views": "0",
    	"comments": "0",
    	"favorites": 1,
    	"isLiked": false,
    	"createdDate": "3 小时前",
    	"excerpt": 
    	  "本文作者：Lin Clark英文原文：Creating and working with WebAssembly modules 本文是关于 WebAssembly 系列的第四篇文章（本系列共六篇文章，后续会将连接补充归整）。如果你没有读先前文章的话，建议先读这里...",
    	"blog": {
		  "id": "1200000008413822",
		  "name": "前端大哈",
		  "url": "/blog/qianduandaha"
	    },
    	"user": {
	        "id": "1030000008186491",
	        "name": "胡子大哈",
	        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/217/801/2178010256-5882edfdd521e_small",
	        "url": "/u/huzidaha",
	        "slug": "dadasa"
    	}
	  },
	  ...
	]
  }
}
```

根据指定 `type` 返回一个 `Article` 对象的列表。除 `hottest` 外，列表总是按照创建时间进行排序，总是将最近的 `Article` 对象显示在最前面。

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 问题列表类型，共4种，`hottest`：最热，`newest`：最新，`recommendable`：推荐的，`tag`：标签 |
**tag** _optional_| String | type 为 `tag` 时必传，填写 tag 的 slug 或者 id |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

## 写文章 [/articles] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1190000008669330",
	"title": "基于Vue2.0高仿微信App·第一期",
	"url": "/a/1190000008669330",
    "currentStatus": "pending",
    "likes": "0",
    "favorites": "0",
    "comments": "0",
    "views": "1",
    "isLiked": false,
    "isFavorited": false,
    "isAuthor": false,
    "isRecommend": true,
    "isDeleted": false,
    "showLicense": false,
    "createdDate": "刚刚",
	"excerpt":
	  "利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 仿3DTouch、登陆、注册、emoji表情内嵌、朋友圈图片查看等功能，让它更接近微信A...",
    "originalText":
      "利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 **仿3DTouch**、**登陆**、**注册**、**emoji表情内嵌**、**朋友圈图片查看**等功能，让它更接近微信App的用户交互体验。\n\n仓库地址：https://github.com/zhaohaodang/vue-WeChat.git\n\n## 手机预览\n首选红色，加载较快 <2018-03-02过期> 蓝色为备胎，加载较慢\n\n!.....",
    "parsedText": 
      "<html><body>\n<p>利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 <strong>仿3DTouch</strong>、<strong>登陆</strong>、<strong>注册</strong>、<strong>emoji表情内嵌</strong>、<strong>朋友圈图片查看</strong>等功能，让它更接近微信App的用户交互体验。</p>\n<p>仓库地址：<a href=\"https://github.com/zhaohaodang/vue-WeChat.git\">https://github.com/zhaohaodan...</a></p>\n<h2>手机预览</h2>\n<p>首选红色，加载较快 &lt;2018-03-02过期&gt; 蓝色为备胎，加载较慢</p>\n<p>......",
    "blog": {
	  "name": "阿荡",
	  "url": "/blog/zhaohd",
	  "id": "1200000005945481",
	  "isFollowed": false,
	  "description": "个人笔记"
    },
    "tags": [
	  {
		"name": "vue-router",
		"url": "/t/vue-router",
		"id": "1040000004222332",
		"thumbnailUrl": "",
	  },
	  {
		"name": "vuex",
		"url": "/t/vuex",
		"id": "1040000004469904",
		"thumbnailUrl": "",
	  },
    ],
    "user": {
        "id": "1030000005271861",
        "slug": "poq",
        "url": "/u/poq",
        "name": "阿荡同学",
        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/144/466/1444663761-58c125b7be3c4_huge128",
        "ranks": "27",
        "followers": 5,
        "isFollowed": false,
    },
    "suggestions": [
      {
		"id": "1190000006431418",
		"url": "/a/1190000006431418",
		"title": "Vue 初接触实战之账单组件",
		"views": "1.8k",
		"favorites": "46",
		"excerpt": 
		  "Vue作为一个构建数据驱动web界面的库，是去年最火的MVVM风格库之一。Vue的用起来有Angular的影子，把很多自定义指令注入html，又吸收了React的优点和精华。比如与Vue的配套使用的Vuex就是从Redux和Flux中借鉴了不少思路。 Vue从去年的下半年开始火起来，目前在Awesomes前端资源库的热度排行里面处于Top2的位置。得益于更...",
	  },
	  {
		"id": "1190000005787179",
		"url": "/a/1190000005787179",
		"title": "[vue+vuex+vue-router] 强撸一发暗黑风 markdown 日记应用",
		"views": "7.4k",
		"favorites": "106",
		"excerpt": 
		  "容我思考思考文章结构，能够更容易让新手入门，思考的过程中被小编拒了一次，囧。本文将会从项目开发角度出发，由外向内拆解，自顶而下设计 项目地址 效果图 暗黑风是不是很炫～Step by step,follow me~ 知识储备 vue.js 官网教程 vuex 官方教程 核心思想 vue-router 官方教程 webpack 官方教程 node.js 官方 es6 阮一峰...",
	  }
    ],
    "commentsDetail": []
  }
}

```

请求参数 | | |
-------------- | -------------- | -------------- |
**title** | String | 文章的标题，一句话简洁概括文章的主要内容 |
**text** | String | 文章主体部分的原文，即作者撰写的原文 |
**tags** | Array | 与该文章相关的 `tag` 对象列表，最多 5 项，均由用户创建文章时提供 |
**blogId** | Int | 该文章所归纳的专栏 id |

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 修改文章 [/articles] [PUT]

> 返回示例参照写文章

请求参数 | | |
-------------- | -------------- | -------------- |
**articleId** | String | 文章的 id |
**title** | String | 文章的标题，一句话简洁概括文章的主要内容 |
**text** | String | 文章主体部分的原文，即作者撰写的原文 |
**tags** | Array | 与该文章相关的 `tag` 对象列表，最多 5 项，均由用户创建文章时提供 |
**blogId** | Int | 该文章所归纳的专栏 id |

<aside class="notice">
只有登录用户并且为作者才可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 删除文章 [/articles] [DELETE]

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
**articleId** | String | 文章的 id |

<aside class="notice">
只有登录用户并且为作者才可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 搜索问题 [/articles/search] [GET]

> 示例参见文章列表

根据提供的关键词，搜索标题或内容中带有该关键词的问题，返回一个 `Article` 对象的列表。

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 搜索的关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 |

## 文章详情 [/articles/{id}] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1190000008669330",
	"title": "基于Vue2.0高仿微信App·第一期",
	"url": "/a/1190000008669330",
    "currentStatus": "recommend",
    "likes": "1",
    "favorites": 18,
    "comments": "6",
    "viewCount": 602,
    "isLiked": false,
    "isFavorited": false,
    "isAuthor": false,
    "isRecommend": true,
    "isDeleted": false,
    "showLicense": false,
    "createdDate": "1 天前",
	"excerpt":
	  "利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 仿3DTouch、登陆、注册、emoji表情内嵌、朋友圈图片查看等功能，让它更接近微信A...",
    "originalText":
      "利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 **仿3DTouch**、**登陆**、**注册**、**emoji表情内嵌**、**朋友圈图片查看**等功能，让它更接近微信App的用户交互体验。\n\n仓库地址：https://github.com/zhaohaodang/vue-WeChat.git\n\n## 手机预览\n首选红色，加载较快 <2018-03-02过期> 蓝色为备胎，加载较慢\n\n!.....",
    "parsedText": 
      "<html><body>\n<p>利用Vue2.0模仿微信app，努力做到以假乱真的效果。个人独立开发，源码中有详细的注释，为新手提供许多有用的提示信息。后期会增加 <strong>仿3DTouch</strong>、<strong>登陆</strong>、<strong>注册</strong>、<strong>emoji表情内嵌</strong>、<strong>朋友圈图片查看</strong>等功能，让它更接近微信App的用户交互体验。</p>\n<p>仓库地址：<a href=\"https://github.com/zhaohaodang/vue-WeChat.git\">https://github.com/zhaohaodan...</a></p>\n<h2>手机预览</h2>\n<p>首选红色，加载较快 &lt;2018-03-02过期&gt; 蓝色为备胎，加载较慢</p>\n<p>......",
    "blog": {
	  "name": "阿荡",
	  "url": "/blog/zhaohd",
	  "id": "1200000005945481",
	  "isFollowed": false,
	  "description": "个人笔记"
    },
    "tags": [
	  {
		"name": "vue-router",
		"url": "/t/vue-router",
		"id": "1040000004222332",
		"thumbnailUrl": "",
	  },
	  {
		"name": "vuex",
		"url": "/t/vuex",
		"id": "1040000004469904",
		"thumbnailUrl": "",
	  },
    ],
    "user": {
        "id": "1030000005271861",
        "slug": "poq",
        "url": "/u/poq",
        "name": "阿荡同学",
        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/144/466/1444663761-58c125b7be3c4_huge128",
        "ranks": "27",
        "followers": 5,
        "isFollowed": false,
    },
    "suggestions": [
      {
		"id": "1190000006431418",
		"url": "/a/1190000006431418",
		"title": "Vue 初接触实战之账单组件",
		"views": "1.8k",
		"favorites": "46",
		"excerpt": 
		  "Vue作为一个构建数据驱动web界面的库，是去年最火的MVVM风格库之一。Vue的用起来有Angular的影子，把很多自定义指令注入html，又吸收了React的优点和精华。比如与Vue的配套使用的Vuex就是从Redux和Flux中借鉴了不少思路。 Vue从去年的下半年开始火起来，目前在Awesomes前端资源库的热度排行里面处于Top2的位置。得益于更...",
	  },
	  {
		"id": "1190000005787179",
		"url": "/a/1190000005787179",
		"title": "[vue+vuex+vue-router] 强撸一发暗黑风 markdown 日记应用",
		"views": "7.4k",
		"favorites": "106",
		"excerpt": 
		  "容我思考思考文章结构，能够更容易让新手入门，思考的过程中被小编拒了一次，囧。本文将会从项目开发角度出发，由外向内拆解，自顶而下设计 项目地址 效果图 暗黑风是不是很炫～Step by step,follow me~ 知识储备 vue.js 官网教程 vuex 官方教程 核心思想 vue-router 官方教程 webpack 官方教程 node.js 官方 es6 阮一峰...",
	  }
    ],
    "commentsDetail": [
	  {
		"id": "1050000008669702",
		"objectId": "1190000008669330",
		"parsedText": "<p>非常棒，clone下来研究一下，期待一起开发。哈哈</p>",
		"originalText": "非常棒，clone下来研究一下，期待一起开发。哈哈",
		"createdDate": "1 天前",
		"isLiked": false,
		"likes": "0",
		"user": {
		  "id": "1030000005893558",
		  "url": "/u/liumin_1",
		  "name": "前端小白de窝",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/223/944/22394488-578605e5cc4ea_big64"
		},
	  },
	  {
		"id": "1050000008669705",
		"userId": "1030000005893558",
		"objectId": "1190000008669330",
	  	"parsedText": "<p>我可以把vue的项目打包成安卓+ios的app</p>",
	  	"originalText": "我可以把vue的项目打包成安卓+ios的app",
	  	"createdDate": "1 天前",
	  	"isLiked": false,
	  	"likes": "0",
	  	"user": {
		  "id": "1030000005893558",
		  "url": "/u/liumin_1",
		  "name": "前端小白de窝",
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/223/944/22394488-578605e5cc4ea_big64"
		},
	  },
	  ...
    ]
  }
}

```

发起一个查询文章的请求，返回一个 `Article` 对象的所有属性。

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 文章赞赏列表 [/articles/{id}/rewards] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"rows": [
	  {
		"amounts": "200",
		"type": "user",
		"user": {
		  "id": "1030000006157187",
		  "url": "/u/cridj"，
		  "name": "helloo",
		  "slug": "cridj",
		  "ranks": "2",
		  "followers": "4",
		  "isEachFollowed": false,
		  "isFollowed": false,
		  "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/249/374/2493745047-58a5702e368c8_big64"
		}
	  },
	  ...
	]
  }
}
```

返回说明 | | |
-------------- | -------------- | -------------- |
**amounts** | String | 单次打赏金额的值 |
**type** | String | 打赏者的类型，共 n 种 (`user` 用户) |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 赞赏文章 [/articles/{id}/rewards] [POST]

> 返回示例

``` json

```

[Ping++ API文档](https://www.pingxx.com/api)

请求参数 | | |
-------------- | -------------- | -------------- |
**amounts** | String | 单次打赏金额的值 |
**paymentMethod** | String | 打赏方式的选择，共 2 种( `wechat` 微信， `alipay` 支付宝) |

<aside class="notice">
当前为登录状态的用户，必须在 Request Header 中带上 Authorization。
</aside>

## 文章评论列表 [/articles/{id}/comments] [GET]

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

## 评论文章 [/articles/{id}/comments] [POST]

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

## 删除文章评论 [/articles/{id}/comments] [DELETE]

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

## 收藏文章 [/articles/{id}/favorites] [POST]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFavorited": true,
    "favorites": "3"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消收藏文章 [/articles/{id}/favorites] [DELETE]

> Response示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFavorited": false,
    "favorites": "2"
  }
}
```

<aside class="notice">
只有登录用户可以请求，必须在 Request Header 中带上 Authorization
</aside>

## 点赞文章 [/articles/{id}/likes] [POST]

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

## 取消点赞文章 [/articles/{id}/likes] [DELETE]

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

## 举报文章 [/articles/{id}/report] [POST]

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



