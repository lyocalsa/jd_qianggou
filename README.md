## 可用于 JD 抢购

## Bugfix

- [x] 购物车无商品时报错
- [ ] 确认订单页-有京豆，提交订单失败

## TODO

- [x] 自动获取 cookie
- [x] 单商品抢购失败后监控下单
- [x] 定时器实现改造（setTimeout 实际执行时间出入很大）
- [ ] 直接购买（去掉购物车流程）
- [ ] 多商品 7\*24 监控

### python 版本可使用 pyinstaller -F -w xx.py 打包为可执行文件，文件在 dist 下，打包后文件在 windows 下运行可直接运行

### 各版本说明。

h5taobao 暂不可用

### JD 版本：

#### v1 和 v2 版，python 实现（不再维护）

v1 版的商品会自动加入购物车，原理是调用加入购物车后，商品在购物车中是默认选中状态，再调用确认订单，最后提交订单。

v2 版是手动加入购物车（这个可以百度下 jd 如何在预约阶段加车），随后调用购物车全选接口，再调用确认订单，最后提交订单。

两者的区别在于加入购物车接口和全选购物车接口的耗时，推荐 v2 版。

v1、v2 只保证单流程走通，v3 增加自动获取 cookie、监控抢单等。推荐 v3 版

#### v3 版，Node 实现（推荐）。

安装依赖：`npm i`
启动命令：`npm run qiang`

根据需要修改配置

```js
// config.js
module.exports = {
  pid: '10035529205226', // 商品ID
  time: '2021-08-19 01:03:30', // 抢购时间
  pcount: 1, // 商品数量
  timeSleep: 100, // 倒计抢购时间轮询间隔，0-1000，默认配置100，越小离抢购时间越精确，但CPU占用也越高，视电脑性能设置。
  timeCut: 500, // 首次抢购失败后，切换为监控模式，监控间隔时间，0或‘'则不监控
};
```

### 前置步骤：清空购物车，减少其他商品干扰

### 总体步骤如下：获取 cookie->获取商品 ID->设置抢购时间和数量->开始抢单

### 第一步：获取 cookie

登录 pc 版 JD 商城，进入购物车，打开控制台，查看接口
https://api.m.jd.com/api?functionId=pcCart_jc_getCurrentCart
的 cookie，填入 cookie 的输入框

v3 版则是赋值给 cookie

```
// index.js 第16行
let cookie = ''; // JD cookie
```

### 第二步：获取商品 id

找到需要抢购的商品，查看详情，可以看到浏览器的 URL 为
https://item.jd.com/xxxxxxxx.html，
复制 xxxxxxxx 填入商品 ID 框，

### 第三步：设置抢购时间和数量

抢购时间需要格式设置，格式为 yyyy-MM-dd HH:mm:ss，如 2021-11-02 12:00:00。数量可随意设置，但需要考虑到店铺的库存以及是否设置为限购 1 件。

### 第四步：开始抢单

这个时候可以泡一杯茶，静待好事发生。
