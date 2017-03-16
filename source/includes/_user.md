# User 用户

`User`是个用户对象对象，所有用户的主要信息都存储在这个对象中，可以注册请求来创建一个新的 `User` 对象，发起修改个人信息的请求去更新 `User` 对象的信息。每个 `User` 对象都拥有一个标识 `id` 或 `slug`，`id` 在系统内唯一且不可修改，`slug` 唯一但可修改。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的问题对象 ID，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 用户的昵称，90天内只可修改 1 次 |
**slug** | String | 用户的slug，用户可自定义的标识符，90天内只可修改 1 次 |
**avatarUrl** | String | 用户头像的 url |
**birthday** | String | 用户的生日 |
**city** | String | 用户所在的城市 |
**desc** | String | 用户的个人描述 |
**site** | String | 用户的个人主页 |
**mail** | String | 用户绑定的邮箱，用***替换部分地址 |
**phone** | String | 用户绑定的手机号码，用***替换部分地址 |
**gender** | Int | 用户的性别，共 3 种固定值（ `0`：保密，`1`：男性，`2`：女性） |
**lastUpdateName** | Int | 距离上次修改名称的时间，以 `天` 为单位，`-1` 为从未修改过 |
**lastUpdateSlug** | Int | 距离上次修改 `slug` 的时间，以 `天` 为单位，`-1` 为从未修改过 |
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
**activeTags** | Array | 该用户活跃的标签，由一个或多个标签组成 |
**skills** | Array | 该用户擅长的技能，由一个或多个组成 |
**projects** | Array | 该用户的项目经验 |
**schools** | Array | 该用户的教育经历 |
**companies** | Array | 该用户的工作经历 |
**thirdBindings** | Array | 该用户绑定的第三方平台 |

## 注册 [/user/register] [POST]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": ""
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
**name** | String | type = `register`时需传入，验证注册时名称是否已存在 |

## 登录 [/user/login] [POST]

> 示例返回

``` json
{
  "status": 0,
  "message": "",
  "data": {
	"token": ""
  }
}
```

请求参数 | | |
-------------- | -------------- | -------------- |
**account** | String | 用户登录的账号，可支持邮箱与手机号 |
**password** | String | 用户登录密码 |

## 退出登录 [/user/logout] [GET]

## 个人信息 [/user/{slug}] [GET]

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

## 取消关注用户 [/user/{slug}/follows] [DELETE]

## 用户粉丝列表 [/user/followers] [GET]

> 返回示例参照我关注的用户列表

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 添加教育经历 [/user/schools] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**profession** | String | |

## 修改教育经历 [/user/schools] [PUT]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**profession** | String | |

## 删除教育经历 [/user/schools] [DELETE]


## 添加工作经历 [/user/companies] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**major** | String | |

## 修改工作经历 [/user/companies] [GET]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**major** | String | |

## 删除工作经历 [/user/companies] [DELETE]

## 添加项目经验 [/user/projects] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**desc** | String | |

## 修改项目经验 [/user/projects] [PUT]

请求参数 | | |
-------------- | -------------- | -------------- |
**name** | String |  |
**desc** | String | |

## 删除项目经验 [/user/projects] [DELETE]

## 上传头像 [/user/avatars] [POST]

## 修改擅长技能 [/user/skills] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**tags** | Array | 用户修改后的擅长技能，由一个或多个组成，没有时传空 |

## 获取用户的私信列表 [/user/messages] [GET]

请求参数 | | |
-------------- | -------------- | -------------- |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 获取用户的消息事件列表 [/user/events] [GET]

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 消息时间的类型，共 3 种(`notify`：通知，`like`：点赞，`follow`：关注) |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 

## 更改用户密码 [/user/password] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**password** | String | 账户原密码 |
**newPassword** | String | 账户新密码 |

## 验证原邮箱 [/user/mail/verify] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**mail** | String | 用户原邮箱的完整地址，用于修改邮箱时验证 |

## 修改用户邮箱 [/user/mail/reset] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**mail** | String | 用户修改后的邮箱地址 |

## 用户的小红点 [/user/read] [GET]

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 用户未读信息的类型，共 2 种（`event`：消息，`message`：私信） |

## 小红点已读 [/user/read] [POST]

请求参数 | | |
-------------- | -------------- | -------------- |
**type** | String | 用户想要置为已读信息的类型，共 2 种（`event`：消息，`message`：私信） |

## 用户搜索 [/user/search] [GET]

> 返回示例参照我关注的用户列表

请求参数 | | |
-------------- | -------------- | -------------- |
**q** | String | 用户的搜索关键字 |
**page** | Int | 列表当前页面的标识，按 `pageSize` 将列表划分成多页，最小为1 |
**pageSize** _optional_ | Int | 限制有多少对象可以被返回，默认 20 项 | 





