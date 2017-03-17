# User 用户

`User`是个用户对象对象，所有用户的主要信息都存储在这个对象中，可以注册请求来创建一个新的 `User` 对象，发起修改个人信息的请求去更新 `User` 对象的信息。每个 `User` 对象都拥有一个标识 `id` 或 `slug`，`id` 在系统内唯一且不可修改，`slug` 唯一但可修改。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 用户的昵称，90天内只可修改 1 次 |
**slug** | String | 用户的slug，用户可自定义的标识符，90天内只可修改 1 次 |
**avatarUrl** | String | 用户头像的 url |
**city** | String | 用户所在的城市 |
**desc** | String | 用户的个人描述 |
**site** | String | 用户的个人主页 |
**mail** | String | 用户绑定的邮箱，用***替换部分地址 |
**phone** | String | 用户绑定的手机号码，用***替换部分地址 |
**gender** | Int | 用户的性别，共 3 种固定值（ `0`：保密，`1`：男性，`2`：女性） |
**lastUpdateNameDays** | Int | 距离上次修改名称的时间，以 `天` 为单位，`-1` 为从未修改过 |
**lastUpdateSlugDays** | Int | 距离上次修改 `slug` 的时间，以 `天` 为单位，`-1` 为从未修改过 |
**ranks** | Int | 用户的个人声望值 |
**followers** | Int | 关注该用户的粉丝数量 |
**followings** | Int | 该用户关注的其他用户数 |
**questions** | Int | 用户提出的问题数 |
**answers** | Int | 用户回答的问题数 |
**blogs** | Int | 用户开通的专栏数 |
**articles** | Int | 用户撰写的文章数 |
**shares** | Int | 用户分享的头条数 |
**notes** | Int | 用户记的笔记数 |
**favorites** | Int | 用户创建的收藏夹数 |
**isFollowed** | Bool | 是否关注该用户 |
**isEachFollowed** | Bool | 是否与该用户互相关注 |
**badges** | Array | 勋章统计，共 3 项 （金勋章，银勋章，铜勋章） |
**activeTags** | Array | 该用户活跃的标签，由一个或多个标签组成 |
**skills** | Array | 该用户擅长的技能，由一个或多个组成 |
**projects** | Array | 该用户的项目经验 |
**schools** | Array | 该用户的教育经历 |
**companies** | Array | 该用户的工作经历 |
**thirdPartyBindings** | Array | 该用户绑定的第三方平台 |

## 注册 [/user/register] [POST]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "token": "8dd12c365125d26bafc4cb0dbc70470c_93dca83281aafe3da1b58201776c5f07"
  }
}
```

请求参数 | | type = `mail` |
-------------- | -------------- | -------------- |
**type** | String | 注册方式，共 2 种（`mail`：邮箱注册） |
**name** | String | 注册时填写的用户名称 |
**mail** | String | 邮箱地址，注册成功后即与账号绑定，可用于登录 |
**password** | String | 用户输入的密码 |


请求参数 | | type = `phone` |
-------------- | -------------- | -------------- |
**type** | String | 注册方式，共 2 种（`phone`：手机注册） |
**name** | String | 注册时填写的用户名称 |
**phone** | String | 手机号码，注册成功后即与账号绑定，可用于登录 |
**code** | String | 手机号所收到的验证码 |
**password** | String | 用户输入的密码 |


## 获取验证码 [/user/phone/code] [POST]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 注册方式，共 5 种（`register`：注册前验证手机，`verify`：更换手机时验证原手机，`reset`：更换手机时验证新手机号，`forget`：手机找回密码验证，`bind`：绑定手机号验证 ）|
**phone** | String | 获取验证码的手机号，暂只支持大陆手机号 |
**name** _optional_| String | type = `register` 时需传入，验证注册时名称是否已存在 |

## 登录 [/user/login] [POST]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "token": "8dd12c365125d26bafc4cb0dbc70470c_93dca83281aafe3da1b58201776c5f07"
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**account** | String | 用户登录的账号，可支持邮箱与手机号 |
**password** | String | 用户登录密码 |

## 退出登录 [/user/logout] [GET]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

## 个人信息 [/user/{slug}] [GET]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1030000004958804",
    "name": "testoopser",
    "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_big64",
    "slug": "testoopser",
    "city": "上海",
    "description": "weishenmen",
    "site": "sf.gg",
    "mail": "270437179@qq.com",
    "phone": "",
    "gender": "0",
    "lastUpdateSlugDays": 143,
    "lastUpdateNameDays": 143,
    "ranks": "0",
    "followers": 1,
    "followings": 7,
    "questions": 0,
    "answers": 2,
    "favorites": 2,
    "blogs": 0,
    "articles": 0,
    "shares": 0,
    "notes": 1,
    "isFollowed": false,
    "isEachFollowed": false,
    "badges": {
      "gold": "0",
      "silver": "0",
      "bronze": "2"
    },
    "thirdPartyBindings": [],
    "projects": [
      {
        "name": "这是一个项目aaaaaaa",
        "description": "这是一个项目"
      },
      {
        "name": "这是项目名1",
        "description": "这是项目名45"
      }
    ],
    "schools": [
      {
        "id": "1310000003082844",
        "major": "艺术",
        "name": "西澳大学",
        "from": "",
        "to": "",
      },
      {
        "id": "1310000003078388",
        "major": "锕系",
        "name": "哈尔滨传媒职业学院",
        "from": "",
        "to": ""
      }
    ],
    "companies": [
      {
        "id": "1310000003078311",
        "position": "而我的职位也很长",
        "name": "我的天哪我的公司名字为什么可以这么长长到换行长到挡住了我的职位",
        "from": "2014-07",
        "to": "2016-03"
      },
      {
        "id": "1310000003072312"
        "position": "程序员鼓励师",
        "from": "2014-07",
        "to": "2016-03",
        "name": "杭州拉熊科技有限公司"
      }
    ],
    "activeTags": [
      {
        "id": "1040000000090869",
        "url": "/t/test",
        "name": "test",
        "incr": "2",
        "iconUrl": ""
      },
      {
        "id": "1040000004337092",
        "url": "/t/testing",
        "name": "testing",
        "incr": "1",
        "iconUrl": ""
      },
      {
        "id": "1040000000719757",
        "url": "/t/php%E6%A1%86%E6%9E%B6",
        "name": "php框架",
        "incr": "1",
        "iconUrl": ""
      }
    ],
    "skills": [
      {
        "id": "1040000000089449",
        "name": "java",
        "url": "/t/java"
      },
      {
        "id": "1040000000089387",
        "name": "php",
        "url": "/t/php"
      }
    ]
  }
}
```
<aside class="notice">
当前为登录用户状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 修改个人信息 [/user/{slug}] [PATCH]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** _optional_ | String | 修改后的用户名称 |
**gender**  _optional_| Int | 修改后的用户性别，共 3 种固定值（ `0`：保密，`1`：男性，`2`：女性） |
**birthday** _optional_ | String | 修改后的用户生日 |
**desc** _optional_ | String | 修改后的个人描述 |
**site** _optional_ | String | 修改后的个人主页 |
**city** _optional_ | String | 修改后的用户所在城市 |
**slug** _optional_ | String | 修改后的slug |

<aside class="notice">
只有登录用户能发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 获取用户的提问列表 [/user/{slug}/questions] [GET]

> 返回示例

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
  	    "answerers": "7",
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

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的回答列表 [/user/{slug}/answers] [GET]

> 返回示例

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
  	    "answerers": "7",
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

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的专栏列表 [/user/{slug}/blogs] [GET]

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
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的文章列表 [/user/{slug}/articles] [GET]

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

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的分享列表 [/user/{slug}/shares] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
    "id": "1210000008691272",
    "title": "一位月收入7000开发者的技术选型",
    "url": "/p/1210000008691272",
    "description": 
      "\n<p>昨天看到有人在研究技术选型，于是自己也写了一个列表。</p>\n<p>所有服务均以高稳定性和低成本作为前提而考虑，适合个人学习和低成本创业使用。</p>\n",
    "currentStatus": "available",
    "likes": "3",
    "comments": "0",
    "createdDate": "4 小时前",
    "isLiked": false,
    "thumbnailUrl": null,
    "type": "url",
    "user": {
      "id": "1030000002377284",
      "name": "利维坦少女",
      "url": "/u/catscarlet",
      "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/255/540/2555403060-55d8ba52c6b94_big64"
    },
    "channel": "程序员"
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

## 获取用户的最新动态 [/user/{slug}/timeline] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "url": "/u/christoph",
        "triggerType": "user",
        "title": "Christoph",
        "createdDate": "1 天前",
        "sentence": "高阳Sunny 关注了用户",
        "excerpt": "浙江财经大学数据分析和大数据计算客座教授，德国不莱梅大学数学博士",
        "actionName": "follow_user",
        "detailSentence": "<a target=\"_blank\" href=\"/u/sunny\">高阳Sunny</a> 关注了用户",
        "object": {
            "id": "1030000008520536",
            "name": "Christoph",
            "status": "0",
            "slug": "christoph",
            "url": "/u/christoph",
            "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/237/061/2370613837-58c1300bf2d46_big64",
            "description": "浙江财经大学数据分析和大数据计算客座教授，德国不莱梅大学数学博士"
        },
        "meta": {
            "followers": 2
        },
        "trigger": {
            "id": "1030000000091294",
            "name": "高阳Sunny",
            "slug": "sunny",
            "url": "/u/sunny",
            "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/373/745/3737454955-5493d7d24ab19_big64"
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

## 获取用户的笔记列表 [/user/{slug}/notes] [GET]

>  返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
  "rows": [
    {
    "id": "1330000008703409",
    "title": "正则表达式规则",
    "url": "/n/1330000008703409",
    "excerpt": 
      "```\n表1.常用的元字符 \n代码\t说明\n.\t匹配除换行符以外的任意字符\n\\w\t匹配字母或数字或下划线或汉字\n\\s\t匹配任意的空白符",
    "language": "markdown",
    "createdDate": "1 分钟前",
    "forks": "0",
    "favorites": "0",
    "isPrivate": false,
    "user": {
      "name": "testoopser",
      "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/259/155/2591555999-580475c6d6762_big64",
      "url": "/u/testoopser"
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

## 获取用户的收藏夹列表 [/user/{slug}/favorites] [GET]

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
**objectId** _optional_ | String | 条目的 id，用于鉴别该条目是否已收藏于收藏夹中 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的关注列表 [/user/{slug}/followings] [GET]

> 关注的用户列表返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "name": "oopser",
        "slug": "oopser",
        "id": "1030000004603175",
        "url": "/u/oopser",
        "ranks": "10",
        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/216/903/2169036367-5747f79e989b9_big64",
        "followers": "8",
        "isEachFollowed": false
      },
      {
        "name": "Fera",
        "slug": "anrious",
        "id": "1030000002768330",
        "url": "/u/anrious",
        "ranks": "22",
        "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/291/997/2919977929-56a76b0ee306b_big64",
        "followers": "23",
        "isEachFollowed": false
      },
      ...
    ]
  }
}
```

> 关注的标签列表返回示例

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

> 专栏列表参照用户的专栏列表

> 问题列表参照用户的问题列表

> 收藏夹列表参照用户的收藏夹列表

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 关注列表的类型，共 5 种(`user`：用户，`blog`：专栏，`question`：问题，`tag`：标签，`favorite`：收藏夹) |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 



## 关注用户 [/user/{slug}/follows] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFollowed": true,
    "isEachFollowed": false,
    "followers": "12"
  }
}
```

<aside class="notice">
只有登录用户可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 取消关注用户 [/user/{slug}/follows] [DELETE]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "isFollowed": false,
    "isEachFollowed": false,
    "followers": "11"
  }
}
```

<aside class="notice">
只有登录用户可以发起请求，必须在 Request Header 中带上 Authorization
</aside>

## 用户粉丝列表 [/user/followers] [GET]

> 返回示例参照我关注的用户列表

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

<aside class="notice">
当前为登录用户状态的用户，必须在 Request Header 中带上 Authorization
</aside>

## 添加教育经历 [/user/schools] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1310000003082844",
    "major": "艺术",
    "name": "西澳大学",
    "from": "",
    "to": "",
  },
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String | 学校的名称，必须从 `/schools/search` 中搜索获得 |
**major** | String | 在学校所学的专业 |
**from** | String | 入学日期，YY-mm，例：2009-09 |
**to** | String | 毕业日期，YY-mm，例：2013-06 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 修改教育经历 [/user/schools] [PUT]

> 返回示例参照添加教育经历

请求参数 | | |
-------------- | -------------- | -------------- |
**schoolId** | String | 需要修改的学校 id，在创建时由 SegmentFault 系统生成 |
**name** | String | 学校的名称，例：浙江工业大学 |
**major** | String | 在学校所学的专业，例：计算机科学与技术 |
**from** | String | 入学日期，YY-mm，例：2009-09 |
**to** | String | 毕业日期，YY-mm，例：2013-06 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 删除教育经历 [/user/schools] [DELETE]

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
**schoolId** | String | 需要移除的学校 id，在创建时由 SegmentFault 系统生成 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 添加工作经历 [/user/companies] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1310000003082844",
    "job": "程序员鼓励师",
    "name": "西澳科技有限公司",
    "from": "",
    "to": "",
  },
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String | 工作期间所在单位的名称，例：杭州堆栈科技有限公司 |
**job** | String | 工作期间在单位岗位名称，例：iOS工程师 |
**from** | String | 入职日期，YY-mm，例：2009-09 |
**to** | String | 离职日期，YY-mm，例：2013-06 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 修改工作经历 [/user/companies] [GET]

> 返回示例参照添加工作经历

请求参数 | | |
-------------- | -------------- | -------------- |
**companyId** | String | 需要修改的单位 id，在创建时由 SegmentFault 系统生成 |
**name** | String | 工作期间所在单位的名称，例：杭州堆栈科技有限公司 |
**job** | String | 工作期间在单位岗位名称，例：iOS工程师 |
**from** | String | 入职日期，YY-mm，例：2009-09 |
**to** | String | 离职日期，YY-mm，例：2013-06 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 删除工作经历 [/user/companies] [DELETE]

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
**companyId** | String | 需要修改的单位 id，在创建时由 SegmentFault 系统生成  |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 添加项目经验 [/user/projects] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "id": "1310000003082844",
    "name": "SegmentFault",
    "desc": ""
  },
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String | 项目的名称 |
**desc** | String | 项目的主要功能及其他描述 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 修改项目经验 [/user/projects] [PUT]

> 返回示例参照添加项目经验

请求参数 | | |
-------------- | -------------- | -------------- |
**projectId** | String | 需要修改的项目 id，在创建时由 SegmentFault 系统生成  |
**name** | String | 项目的名称 |
**desc** | String | 项目的主要功能及其他描述 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 删除项目经验 [/user/projects] [DELETE]

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
**projectId** | String | 需要删除的项目 id，在创建时由 SegmentFault 系统生成  |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 上传头像 [/user/avatars] [POST]

## 修改擅长技能 [/user/skills] [POST]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    skills: [
      {
        "id": "1040000000089449",
        "name": "java",
        "url": "/t/java"
      },
      {
        "id": "1040000000089387",
        "name": "php",
        "url": "/t/php"
      }
    ]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**tags** | Array | 用户修改后的擅长技能，由一个或多个 `tag` 对象的 `id` 组成，没有时传空 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 获取用户的私信列表 [/user/messages] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "id": "1430000007295053",
        "url": "/inbox/1430000007295053",
        "sentence": "和SegmentFault 团队的私信",
        "viewed": 1,
        "createdDate": "2016年10月27日",
        "user": {
          "name": "SegmentFault 团队",
          "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/569/558/569558099-1030000000094051_huge256",
          "url": "javascript:;",
          "isBlocked": false
        },
        "lastMessage": {
          "content":
            "SegmentFault 讲堂产品正式上线，大家以后可以在社区看在线的技术分享了 ：https://segmentfault.com/lives/will \n\n讲堂推荐：\n\n1：web 安全之 xss 漏洞攻击 https://segmentfault.com/l/1500000008510353\n2：前端工程师的自我修养 https://segmentfault.com/l/1500000008524402\n3：深入剖析 iOS 编译 Clang / LLVM https://segmentfault.com/l/1500000008514518"
          "createdDate": "3月6日"
        }
      },
      ...
    ]
  }
}
```

请求时即让主站的提示未读小红点消失，详情条目的未读置为已读功能需发起“忽略”请求

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 获取用户的消息事件列表 [/user/events] [GET]

> `notify` 通知事件 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "id": "1418807",
        "excerpt": "新手上路",
        "url": "/b/1120000000161477?_ea=1418807&userId=1030000004958804",
        "sentence": "你获得了新徽章",
        "detail": 
          "你获得了新徽章 <a href=\"/b/1120000000161477?_ea=1418807&userId=1030000004958804\">新手上路</a>"
        "viewed": "1",
        "currentStatus": "available",
        "createdDate": "2016年12月02日",
        "type": "37"
      },
      {
        "id": "1371599",
        "excerpt": "关于VUEX2.0中的mapMutations的问题",
        "url": "/q/1010000007518447?_ea=1371599",
        "sentence": "NeoChang 回答了问题 ",
        "detail": 
          "<a href=\"/u/neochang\">NeoChang</a> 回答了问题 <a href=\"/q/1010000007518447?_ea=1371599\">关于VUEX2.0中的mapMutations的问题</a>"
        "currentStatus": "available",
        "createdDate": "2016年11月18日",
        "viewed": "1",
        "type": "29"
      },
    ]
  }
}
```

> `like` 点赞事件 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "id": "1699630",
        "excerpt": "乔布斯：库克你做得对，我终于可以安息了",
        "url": "/p/1210000008622402?_ea=1699630",
        "sentence": "h386926074 赞了你的评论",
        "detail": 
          "<a href=\"/u/h386926074\">h386926074</a> 赞了你的评论 <a href=\"/p/1210000008622402?_ea=1699630\">乔布斯：库克你做得对，我终于可以安息了</a>",
        "createdDate": "3月9日",
        "viewed": "1",
        "type": "34",
      },
      {
        "id": "1649693",
        "excerpt": "Aspects AOP 的实现",
        "url": "/a/1190000008020853?_ea=1649693",
        "sentence": "crisitina 赞了你的评论",
        "detail": 
          "<a href=\"/u/_natie_\">crisitina</a> 赞了你的评论 <a href=\"/a/1190000008020853?_ea=1649693\">Aspects AOP 的实现</a>",
        "createdDate": "2月22日",
        "viewed": "1",
        "type": "34",
      },
      ...
    ]
  }
}
```

> `follow` 关注事件 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "rows": [
      {
        "id": "1578581",
        "detail": "<a href=\"/u/lvye\">Lvye</a> 关注了你",
        "url": "/u/testoopser?_ea=1578581",
        "viewed": "1",
        "createdDate": "1月23日",
        "user": {
          "id": "1030000000324613",
          "name": "Lvye",
          "url": "/u/lvye",
          "isFollowed": false,
          "isEachFollowed": false,
          "ranks": "1946",
          "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/374/240/374240081-582d4daa5b4ce_big64",
        }
      },
      {
        "id": "1515071",
        "detail": "<a href=\"/u/gemini\">Gemini</a> 关注了你",
        "url": "/u/testoopser?_ea=1515071",
        "viewed": "0",
        "createdDate": "1月3日",
        "user": {
          "id": "1030000000199113",
          "name": "Gemini",
          "url": "/u/gemini",
          "isFollowed": true,
          "isEachFollowed": true,
          "ranks": "6524",
          "avatarUrl": "https://sfault-avatar.b0.upaiyun.com/345/679/3456790589-575d08ad437b0_big64",
        }
      },
      ...
    ]
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 消息时间的类型，共 3 种(`notify`：通知，`like`：点赞，`follow`：关注) |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 更改用户密码 [/user/password] [POST]

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
**password** | String | 账户原密码 |
**newPassword** | String | 账户新密码 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 验证原邮箱 [/user/mail/verify] [POST]

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
**mail** | String | 用户原邮箱的完整地址，用于修改邮箱时验证 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 修改用户邮箱 [/user/mail/reset] [POST]

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
**mail** | String | 用户修改后的邮箱地址 |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 消息或私信列表的已读 [/user/read] [GET]

> 返回示例

``` json
{
  "status": 0,
  "message": "",
  "data": {
    "notifyListRead": false,
    "likeListRead": false,
    "followListRead": false,
    "messageListRead": true
  }
}
```

该请求是获取 `消息事件` 或 `私信` 中的是否有未查看的`列表`，即小红点提示，该信息在发起 `消息事件列表` 或 `私信列表` 请求后即置为 `1`，视为该列表已读。

例：

- 初次发起 `/user/read [GET]` 请求，返回 `messageListRead: true`，表示我在 `私信列表` 中有未读消息并且未能查看此消息列表。
- 发起 `/user/events?type=message [GET]` 请求，返回我的私信中含有 3 条用户私信记录（其中 2 条未读，1 条已读）。
- 再次发起 `/user/read [GET]` 请求，返回 `messageListRead: false`，表示我已查看私信列表，不能知道我是否已读私信列表中的条目。


请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 用户未读信息的类型，共 2 种（`event`：消息，`message`：私信） |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 忽略消息或私信 [/user/ignored] [POST]

``` json
{
  "status": 0,
  "message": "",
  "data": ""
}
```

该请求是将 `消息事件` 或 `私信` 中的所有条目置为已读。

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 用户想要置为已读信息的类型，共 2 种（`event`：消息，`message`：私信） |

<aside class="notice">
必须在 Request Header 中带上 Authorization
</aside>

## 用户搜索 [/user/search] [GET]

> 返回示例参照我关注的用户列表

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 用户的搜索关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 





