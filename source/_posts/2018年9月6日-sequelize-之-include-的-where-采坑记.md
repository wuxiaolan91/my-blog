title: 2018年9月6日 sequelize 之 include 的 where 采坑记
author: Xiaolan Wu
date: 2018-09-06 15:19:56
tags:
---
## 一.需求
在我们小程序的首页, 需要显示某个分类下的约稿函

![约稿函列表](http://assets.ytougao.com/WX20180906-155823@2x.png)

在这个接口里,会在 include 里带上它 explore 的 id, 然后我在小程序里判断一个约稿函对象的 explores数组大于0,就表示这家公众号有探路帖.

但是我发现一个问题.比如"一千灵异夜"这家公众号,我们小程序里有多款探路帖,所以它在页面上会显示"已探",
但是 *有探路帖不代表就要显示已探, 因为我们的探路帖是要经过我们后台加精,才会显示给用户看的 *

这个就像微信公众号的加精一样.

所以我的需求就是:只有当一家约稿函有加精过的探路帖,才给用户显示已探.

## 二. 遇到的问题

但是当我在 include 的 explore 里加上 
```
    include: [
      {
        model: models.explore,
        attributes: ['id'],
        where: {
          isActive: 1
        },
      }
    ]
```
这里有个筛选条件,我的原意是 where 等于1才返回.
ok. 加上后,我发现返回的约稿函列表不正常了.

仔细一看发现一定是满足它的探路帖里有 isActive 是1的约稿函才会返回.

**what**, 为什么 include 里符合条件的 parent 才会返回. 

也就是说,如果我一篇约稿函下没有加精的探路帖,现在约稿函都不会返回了!


## 解决
搜谷歌,在这里找到了解决方法(github)[https://github.com/sequelize/sequelize/issues/1794]

```
required: false so:
include: [{ model: Profile, where: { profile_name: 'abc' }, attributes: ['profile_name'], required: false }
```

看见木有,其实解决起来很简单,只不过这个问题不是我想的那样(我默认是不会认为子 include 会去对 parent 造成过滤的,像之前我碰到了一个需要include 对 parent 造成过滤,我也是写在 parent 的 where 里)

代码改成这样之后,就好了
``` javascript
    include: [
      {
        attributes: ['id'],
        model: models.explore,
        where: {
          isActive: 1
        },
        required: false // 解决的代码就是这一行,加上 required: false
      }
    ]
```