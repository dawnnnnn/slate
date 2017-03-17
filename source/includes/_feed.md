# Feed 时间线

`Feed`是个状态对象，用户不需要手动发起请求去创建新的 `Feed` 对象，在进行其他对象的操作时，系统会为用户自动生成 `Feed`对象。
用户可以随时查询一个或多个 `Feed` 对象的信息。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的Feed对象 ID |
**url** | String | feed 状态指向的路由，用于事件跳转 |
**type** | String | feed 的类型，共 11 种 （`article`, `question`, `answer`, `tag`, `user`, `share_url`, `share_text`, `blog`, `live`, `activity`, `favorite`）|
**sentence** | String | 状态的描述，例：css3 标签的热门提问 |
**detailSentence** | String | 解析为 HTML 后的状态描述 |
**title** | String | 状态内容的标题，即`article` `question`等对象的标题 |
**excerpt** | String | 状态内容的摘要，即`article` `question`等对象的摘要 |
**actionName** | String | 比 `type` 更细分的动作 |
**createdDate** | String | 根据创建的时间戳解析的时间 |
**triggerType** | String | 触发该状态的对象的类型，共 2 种 (`tag`: 标签， `user`: 用户) |
**trigger** | Object | 触发该状态的对象，与 `triggerType` 对应 |
**blog** | Object | feed 类型为 文章 时有值 |
**meta** | Object | 该状态的标记，如提问的关注数、评论数、是否已解决等，可选择性含有 (`answers`, `likes`, `favorites`, `followers`, `comments`, `isAccept`, `signs`) |
**object** | Object | 该状态的主体对象，一般与 `type` 状态对应 |


## feed 列表 [/feed] [GET]

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
        "type": "user",
        "createdDate": "1 天前",
        "sentence": "高阳Sunny 关注了用户",
        "detailSentence": 
          "<a target=\"_blank\" href=\"/u/sunny\">高阳Sunny</a> 关注了用户",
        "excerpt": 
          "浙江财经大学数据分析和大数据计算客座教授，德国不莱梅大学数学博士",
        "actionName": "follow_user",
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
      {
        "url": "/q/1010000008439888",
        "id": "1030000004603175:1010000008439888",
        "triggerType": "tag",
        "title": "sql索引问题",
        "type": "question",
        "createdDate": "21 分钟前",
        "sentence": "mysql 标签的热门提问",
        "detailSentence": 
          "<a target=\"_blank\" data-id=\"1040000000089439\" href=\"/t/mysql\">mysql</a> 标签的热门提问",
        "excerpt": 
          "有3个语句。 where cid=? where id=? and ownerid=? where cid=? and ownerid=? 现在id已经是主键索引了。请问这样的情况表表应该如何加索引？ 分别对ownerid,cid添加索引吗？ 还有一种情况,另一个表：where cid=? and userid=?where userid=?where cid=?这3个sql语...",
        "actionName": "recommend_tagged_question",
        "object": {
          "id": "1010000008439888",
          "title": "sql索引问题",
          "url": "/q/1010000008439888",
          "status": "0"
        },
        "meta": {
          "followers": 5,
          "answers": "4",
          "isAccepted": false,
          "isFollowed": false,
          "isLiked": false,
          "isBookmarked": false
        },
        "trigger": {
          "id": "1040000000089439",
          "url": "/t/mysql",
          "name": "mysql",
          "thumbnailUrl": "https://sfault-avatar.b0.upaiyun.com/164/722/1647222906-1040000000089439_small"
        },
      },
    ]
  }
}
```
