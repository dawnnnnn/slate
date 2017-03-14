# Blogs 专栏

你可以创建一个 `Blog` 对象来归档自己的文章。在写文章前必须先拥有一个专栏，你可以通过发起创建文章请求来创建一个新的 `Blog` 对象。每个 `Blog` 对象都拥有一个标识 `id`，该 `id` 在系统内唯一。

属性 | | |
-------------- | -------------- | -------------- |
**id** | String | 由 SegmentFault 生成的专栏对象 id，16位数字组成的字符串 |
**url** | String | SegmentFault 指定路由，与主站对应的 path |
**name** | String | 专栏的名称 |
**desc** | String | 专栏的简介，简单概括开专栏的原因或专栏的主要主题，限制长度 |
**currentStatus** | String ||
**isFollowed** | Bool | 表示查看该专栏的用户是否关注了该问题，未登录查看默认状态为 `false` |
**articles** | Int | 该专栏下，已发布文章的数量 |
**followers** | Int | 关注该专栏的用户数量 |
**user** | Object | 创建该专栏的用户对象 |

