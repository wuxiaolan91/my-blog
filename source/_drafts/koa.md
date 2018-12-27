title: koa
author: Xiaolan Wu
date: 2018-08-19 16:58:22
tags:
---
# 我觉得我现在的 nodejs 代码写的很有问题
多个地方引入 sequelize, 并进行链接打开
这样相当于我把 sequelize 的链接在这个项目里打开了14次.
代码如下
每一个 controller 都是这么引入的

```javascript
// 这是 YuegaohanController.js
const Sequelize = require('sequelize');

let db = require('../config/local.config.js');
const sequelize = new Sequelize(db.mysql.DB_URL, {
  define: {
    timestamps: false
  }
});
const Op = Sequelize.Op;
let Hostfunc = require('../models/host.js');
let LabelFunc = require('../models/label.js');
let YuegaohanFunc = require('../models/yuegaohan.js');
let YuegaohanLabelFunc = require('../models/yuegaohan_label.js');
let UserFunc = require('../models/user.js'); // userfunc
let ExploreFunc = require('../models/explore.js'); // userfunc
let YuegaohanStarFunc = require('../models/yuegaohan_star.js');
// host 收藏

let User = UserFunc(sequelize, Sequelize);
let Host = Hostfunc(sequelize, Sequelize);
let Label = LabelFunc(sequelize, Sequelize);
let Explore = ExploreFunc(sequelize, Sequelize);
let Yuegaohan = YuegaohanFunc(sequelize, Sequelize);
let YuegaohanStar = YuegaohanStarFunc(sequelize, Sequelize);
let YuegaohanLabel = YuegaohanLabelFunc(sequelize, Sequelize);
```

代码里类似这样的 controller 我有12个.
所以 sequelize 我要初始化12次,打开连接12次