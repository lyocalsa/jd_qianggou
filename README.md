## 可用于JD抢购

### python版本可使用pyinstaller -F -w xx.py打包为可执行文件，文件在dist下，打包后文件在windows下运行可直接运行

### 各版本说明。
h5taobao 暂不可用

### JD版本：

#### v1和v2版，python实现（不再维护）
v1版的商品会自动加入购物车，原理是调用加入购物车后，商品在购物车中是默认选中状态，再调用确认订单，最后提交订单。

v2版是手动加入购物车（这个可以百度下jd如何在预约阶段加车），随后调用购物车全选接口，再调用确认订单，最后提交订单。

两者的区别在于加入购物车接口和全选购物车接口的耗时，推荐v2版。

v1、v2只保证单流程走通，v3增加自动获取cookie、监控抢单等。推荐v3版

#### v3版，Node实现（推荐）。
安装依赖：``npm i``
启动命令：``npm run qiang``

登录后自动获取cookie
```js
// config.js
// 修改需要抢购的商品ID和时间
module.exports = {
  pid: '10034774689703', // 商品ID
  time: '2021-08-17 23:36:20', // 抢购时间
  pcount: 1, // 商品数量
  timeCut: 500, // 监控间隔时间，0或‘'则不监控
}
```

### 前置步骤：清空购物车，减少其他商品干扰
### 总体步骤如下：获取cookie->获取商品ID->设置抢购时间和数量->开始抢单

### 第一步：获取cookie
登录pc版JD商城，进入购物车，打开控制台，查看接口 
https://api.m.jd.com/api?functionId=pcCart_jc_getCurrentCart
的cookie，填入cookie的输入框

### 第二步：获取商品id
找到需要抢购的商品，查看详情，可以看到浏览器的URL为
https://item.jd.com/xxxxxxxx.html，
复制xxxxxxxx填入商品ID框，

### 第三步：设置抢购时间和数量
抢购时间需要格式设置，格式为yyyy-MM-dd HH:mm:ss，如2021-11-02 12:00:00。数量可随意设置，但需要考虑到店铺的库存以及是否设置为限购1件。

### 第四步：开始抢单
这个时候可以泡一杯茶，静待好事发生。

## 战果
本人鞋迷，目前收获一双大三角、一双闪现3

## TODO
+ [x] 自动获取cookie
+ [x] 监控下单
