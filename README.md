

# pro 和 std 区别
1. pro 是单页应用 通过 #hash 来切换路由  而 std 是多页应用 每个页面都是一个 html 文件
2. 目前更改针对pro  std可以参考修改

# 升级layui 到2.9.27 

2.6.11 调整  参考 https://gitee.com/layui/layui/issues/I5AXSP
1.  {{ d.field }} 默认开启编码  也就是 会加载引号导致多个双引号  影响左侧菜单 {{- d.field }} 就和之前效果一样 {{ 有存在双引号的修改改 }}  
注意 {{- d.field }}  - 要靠近双引号 否则有时候不生效
2.  table 的 escape 属性 默认开启  导致  表格中  有html标签  会被转义  导致显示错误
3. 主要在layout.html 中{{d.field }}修改{{- d.field }}  主要是还有引号  - 保持原样输出  不加引号会xss过滤
4. 2.6的时候所有css和js的合并到一起了. css除了layim 其他的都在 layui.css
5. 2.9.27 升级到2.13.3    侧边栏 点击除第一个菜单  会出现菜单不展开 跳到第一个  原因是 admin.on("hash(side)", function (router) {  router.path 正常的时候是返回3个参数,但是升级到最新版出现4个 第一个是空白字符串  导致匹配失败 修复 var path = router.path  改成var path = router.path.slice(1)  admin.js 和layout.html d都需要修改
6. layui 2.13.3   layim 调整 获取到最新的3.9.9 独立成文件夹包  layui 就是和官方一致 移除gif表情包