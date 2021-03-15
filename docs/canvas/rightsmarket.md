---
title: 权益超市H5前端项目架构
---

#### 集运页面编辑系统

# PC组件H5调试
### 编排系统前端项目架构

##### src目录树
```
tree -I node_modules src -L 3 -I images

src
├── App.vue
├── api
│   ├── common.js
│   ├── comp_login.js
│   ├── goodsdetail.js
│   ├── orderList.js
│   ├── rights.js
│   └── setting.js
├── assets
│   ├── js
│   │   └── vconsole.min.js
│   ├── layout
│   │   ├── detail.json
│   │   ├── login.json
│   │   └── test.json
│   └── rule
│       └── 3.json
├── components
│   ├── HelloWorld.vue
│   ├── SecondConfirmBuy.vue
│   ├── awesomeSwiper.vue
│   ├── detailCard.vue
│   ├── orderItem.vue
│   ├── popup.vue
│   ├── productList.vue
│   ├── quiteLoginDialog.vue
│   └── vipInfoBanner.vue
├── config.js
├── const
│   └── RegionContant.js
├── main.js
├── mixins
│   └── sendDataMixin.js
├── router.js
├── store
│   └── index.js
├── utils
│   ├── application.js
│   ├── auth.js
│   ├── authHelp.js
│   ├── cookie.js
│   ├── crypto.js
│   ├── details.js
│   ├── encrypt.js
│   ├── func.js
│   ├── index.js
│   ├── leadeon.js
│   ├── marketRequest.js
│   ├── request.js
│   ├── requestcoc.js
│   ├── share.js
│   ├── uidlogin.js
│   └── utils.js
└── views
    ├── common
    │   ├── 404.vue
    │   ├── NetworkError.vue
    │   └── rightsInfoSwiper
    │       └── index.vue
    ├── components
    │   ├── IPcontentRecommend
    │   │   └── index.vue
    │   ├── activityRules
    │   │   └── index.vue
    │   ├── alipayLogin
    │   │   ├── img
    │   │   │   └── alipaylogin-preview.jpg
    │   │   ├── index.vue
    │   │   └── scss
    │   │       └── index.scss
    │   ├── backHome
    │   │   └── index.vue
    │   ├── classify
    │   │   └── index.vue
    │   ├── dialog
    │   │   └── index.vue
    │   ├── entrylist
    │   │   └── index.vue
    │   ├── faq
    │   │   └── index.vue
    │   ├── float
    │   │   └── index.vue
    │   ├── flowGet
    │   │   └── index.vue
    │   ├── fourCol
    │   │   └── index.vue
    │   ├── goodsInfo
    │   │   ├── components
    │   │   │   ├── chooseMenu.vue
    │   │   │   ├── payTypeList.vue
    │   │   │   └── vantGoodsSwipe.vue
    │   │   └── index.vue
    │   ├── hot
    │   │   └── index.vue
    │   ├── index.js
    │   ├── login
    │   │   └── index.vue
    │   ├── loginGuide
    │   │   └── index.vue
    │   ├── memberOpening
    │   │   └── index.vue
    │   ├── memberUpgrade
    │   │   └── index.vue
    │   ├── notice
    │   │   └── index.vue
    │   ├── orderList
    │   │   └── index.vue
    │   ├── orderResult
    │   │   └── index.vue
    │   ├── pic
    │   │   └── index.vue
    │   ├── quiteLogin
    │   │   └── index.vue
    │   ├── refresh
    │   │   └── index.vue
    │   ├── richText
    │   │   └── index.vue
    │   ├── rightsGet
    │   │   └── index.vue
    │   ├── rightsHandbook
    │   │   └── index.vue
    │   ├── rightsInfo
    │   │   └── index.vue
    │   ├── search
    │   │   └── index.vue
    │   ├── secKillbanner
    │   │   └── index.vue
    │   ├── swiper
    │   │   └── index.vue
    │   ├── threeMarket
    │   │   └── index.vue
    │   ├── threePicJump
    │   │   └── index.vue
    │   ├── threePicsRecommend
    │   │   └── index.vue
    │   ├── title
    │   │   └── index.vue
    │   ├── top
    │   │   └── index.vue
    │   ├── userInfo
    │   │   └── index.vue
    │   ├── verticalListRecommend
    │   │   └── index.vue
    │   ├── vip
    │   │   └── index.vue
    │   └── wakeupAppToUrl
    │       ├── index.vue
    │       └── js
    │           └── callLib.js
    └── rights
        └── index.vue
```


### 主要渲染逻辑
todo 渲染逻辑重新写

- 1登陆 - 1发送验证码 2账号密码验证码换token
- 2拿到token之后请求application的list接口，把返回的第一个设为当前登陆的平台（**有个问题就是新环境切换的时候后台application的列表是为空的**）
- 3跳转page列表页（**这边会遇到组件渲染的时候list接口返回值还没有拿到的情况，所以watch监听vuex的时候不能加immediate为true**）
- 4选择具体页面进入详情页
- 5详情页组件操作完毕之后点击保存，测试发布 **直接保存仅仅是把数据存到数据库中，发布了才会生成对应页面的json文件**
- 6浏览器网路请求那边调用接口 save 接口 instances字段内容
JSON.stringify(JSON.stringify(specify字段内容))
复制到rightsmarket h5项目 src->assets->layout->test.json
specify字段替换，applicationId最好也换一下

### 获取系统参数方法
在main.js中给vue的原型上添加了bus属性充当事件总线，发布消息时使用$emit('systemConfig', config),订阅消息使用$on('systemConfig', (config) => {})
```javascript
mounted() { // 每个业务组件初始化的时候需要订阅systemConfig消息
    this.bus.$on('systemConfig', (config) => {
        // todo 具体业务逻辑
        this.systemConfig = config // 参考写法 将config中的某个具体参数赋值存到自己组件的data中便于其他方法判断
    })
}
```
### 点击插码之后需要存放上一跳相关信息为下一跳访问插码做准备
/*
        * info 上一跳的组件信息
        * pointPosition   上一跳的位置信息
        * goodsNo   点击商品的mid
        * currentUrl 访问下一跳页面的短链地址
        * pageInfo  上一跳的页面信息
        * */
        let pageInfo = JSON.parse(authHelp.getValue(authHelp.PAGE_INFO))
        localStorage.setItem('jumpInfo', JSON.stringify({info: this.info, pointPosition: index, goodsNo: '', pageInfo}))


### 优化与调试
- 遇到问题先自己想想可能的原因是什么，自己尝试着改一下bug，跳出舒适区
- 改bug  找问题要先定位  
  - 后台接口字段名改了？
  - 前端代码逻辑错误？ 
  - 服务器代理没转发？ 
- 自己的功能开发需要修改别人写的代码
- portal环境遇到的问题
  - k8s 路由代理 /56341495/rightsmarket-h5-canvas/ -> 
	linux服务器实际文件地址 
  - nginx location proxy_pass 代理原理
  
### 学习资源 大家有好的资源可以继续补充
- [基础查询网站mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [Vue 2.x 源码解析](https://vue-js.com/learn-vue/start/)
- [JS深入](https://github.com/mqyqingfeng/Blog)


### 彩蛋
- 要学会善用工具  工具是为了更高效的开发
- 自动换行 
- 代码片段 文件->首选项->用户片段
- gitignore 忽略git监听指定文件类型变化 /dist
- 能看懂简单的正则匹配符号
- webpack插件 postcss-plugin-px2rem 原理
  - vue-config-js rootValue 换算基数 默认100
  - 如果个别地方不想转化px。可以简单的使用大写的 PX 或 Px 。
  - App.vue 中转换html的fontSize
  - 原理 使用rem 针对不同手机屏幕尺寸和dpr动态的改变根节点html的font-size大小(基准值)，再使用fis-postprocessor-px2rem插件让px自动转化成rem
- markdown语法
- 常用的linux操作：cd mkdir cp ls touch 
- 浏览器操作快捷键：ctrl+w 关闭当前页 ctrl+t 打开同窗口新标签页
ctrl+n 打开新窗口新标签页
- windows操作快捷键 win+d 显示桌面
- tree生成目录树
- [练习指法 高效打字](http://www.daziba.cn/zflx/)


```
"Print to console": {
  "prefix": "vue",
  "body": [
      "<template>",
      " <div>\n",
      " </div>",
      "</template>\n",
      "<script>",
      " export default {",
      "   name: '',",
      "   props: {",
      "   },",
      "   components: {\n",
      "   },",
      "   data () {",
      "     return {\n",
      "     }",
      "   },",
      "   methods: {\n",
      "   },",
      "   mounted() {\n",
      "   },",
      "   watch: {\n",
      "   },",
      "   computed: {\n",
      "   },",
      "   filters: {\n",
      "   }",
      " }",
      "</script>\n",
      "<style scoped lang='scss'>\n",
      "</style>"
  ],
}
```
### 一、需求地址
- [需求文档](http://10.71.164.32:8090/pages/viewpage.action?pageId=15076787) 
- [权益超市进度计划表](https://docs.qq.com/sheet/DVXhUb2NWZ0lxU1hF?tab=95ag4r) 

### 二、项目地址
- [编排环境：PC的开发仓库](http://10.70.152.159:4960/base/common/canvas-manager-web)
- [运行环境：H5的开发仓库](http://10.70.152.159:4960/front/business/rightsmarket-h5-canvas)   
  - 注：<br>
1、多个项目共用PC编排环境，使用同一个PC仓库，编排环境PC仓库目前包含系统、权益超市、权益领取，后续还会陆续新增其他站点。<br>
2、H5运行环境（H5仓库）根据不同站点有不同的开发仓库。<br>
3、PC/H5工程本地启动工程后（localhost）默认连的接口是沙箱环境。     

### 三、开发规范
- 1、clone仓库：
```
  git clone http://10.70.152.159:4960/front/business/rightsmarket-h5-canvas.git

  git clone http://10.70.152.159:4960/base/common/canvas-manager-web.git
```

- 注：
如上述无权限尝试：
git clone http://name:password@10.70.152.159:4960/front/business/rightsmarket-h5-canvas
密码中的特殊字符需转义：例如：encodeURIComponent('@')<br/>
<br/>
- 2、分支包含：master（备份）、 release（部署生产）、 sandbox（部署沙箱）、 staging（部署预发）、个人分支（开发各自需求）。
<br/>
- 3、从release分支切出自己的开发分支，格式：名字-时间-修改内容（wgq-20210129-swipper_modify）：在自己的分支中开发，开发好需求后，无报错提交到自己远端分支。部署沙箱：提合并到sandbox分支的MergeRequest给部署人员，通知部署人员部署沙箱；部署预发：提合并到staging分支的MergeRequest给部署人员，通知部署人员部署预发。
<br/>  
  - 注：<br/>
 1、部署人员：<br/>
系统侧：林勤、郑勤园<br/>
权益超市：余芬芬、夏阳、翁江鹏<br/>
权益领取：陈红斌、郑少国<br/><br/>
 2、打包指令：<br>
PC编排环境打包指令：`npm run build:prod`<br/>
H5运行环境打包指令：<br/>
沙箱： `npm run build:sandbox`<br/>
预发： `npm run build:staging`<br/>
生产： `npm run build:prod`<br/><br/>
3、预发环境群里联系运维刘锟部署，生产环境上线当日填写[上线手册](https://docs.qq.com/sheet/DSnJFVFZwY0NMZEhE?newPad=1&newPadType=clone&tab=a1hp50)，生产H5打好包后先邮件发送运维部署CDN，部署完成CDN后再联系运维部署IT。<br/><br/>
 - 4、本地localhost路径 http://localhost:8080/56341495/rightsmarket-h5-canvas/grey/ghtest28?channelCode=00010020
  ，在PC编排环境中可点击页面地址查看对应url，其中grey为测发地址，online为正发地址。<br/>
 - 5、组件开发命名规范、目录结构以及具体代码实现参考权益超市现有组件，站点组件需先在 https://docs.qq.com/sheet/DVWhiTUVkampKbEhq?tab=7o7vuu&_t=1613977679952 中做好统计。<br/>
 - 6、PC开发仓库中组件结构目录为：src-views-components-rights-xxx，具体组件中包含img图片文件夹，edit.vue文件为页面编辑管理-编辑页面-右侧属性区域，index.vue为组件本身（H5使用的即是此文件）；H5开发仓库组件结构目录为：src-views-components-xxx。
 - 7、在PC开发仓库中开发完成新组件后，把rights下的新加组件，复制到H5开发仓库的components下，删除edit.vue，启动H5项目测试是否有异常，投产前把使用到的图片邮件发给运维部署到CDN，H5中使用的图片和打包后的部署文件要求均为CDN。


 ### 四、环境部署和访问
 - 1、localhost环境：<br>
    编排环境：PC：http://localhost:9528/#/page/manage<br>
    运行环境：H5：http://localhost:8080/56341495/rightsmarket-h5-canvas/grey/ghtest28?channelCode=00010020
 - 2、沙箱环境：<br>
    编排环境：PC：https://sandbox.open.10086.cn/56341495/canvas-manager-web/#/<br>
    运行环境：H5：https://sandbox.open.10086.cn/56341495/rightsmarket-h5-canvas/grey/ghtest28
 - 3、预发环境：<br>
    编排环境：PC：https://dev.coc.10086.cn/staging-coc3/canvas/canvas-manager-web/#/<br>
    运行环境：H5：https://dev.coc.10086.cn/staging-coc3/canvas/rightsmarket-h5-canvas/online/mine
 - 4、生产环境：<br>
    编排环境：PC：https://dev.coc.10086.cn/coc3/canvas/canvas-manager-web/#/<br>
    运行环境：H5：https://dev.coc.10086.cn/coc3/canvas/rightsmarket-h5-canvas/online/mine<br>
(grey测试用，online正式用)
   - 注：<br>
      1、PC的沙箱环境账号密码：<br>
      账号：testuser<br>
      密码：testpassword<br>
      验证码：123456<br>
      2、https://dev.coc.10086.cn/staging-coc3/canvas/rightsget-h5-canvas/grey/home?debug=1  url后带debug=1则打开 vconsole，方便调试。


### 五、测试流程
 - 1、localhost自测PC+H5
 - 2、沙箱环境自测PC+H5
 - 3、预发环境自测PC+H5
 - 4、产品组测试
 - 5、测试组测试


### 六、bug管理
 - [产品验收的bug列表](
https://docs.qq.com/sheet/DVWhiTUVkampKbEhq?tab=s60usw&_t=1613977679952)


### 七、学习资源 大家有好的资源可以继续补充
- [基础查询网站mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)
- [Vue 2.x 源码解析](https://vue-js.com/learn-vue/start/)
- [JS深入](https://github.com/mqyqingfeng/Blog)


### 八、彩蛋
- webpack插件 postcss-plugin-px2rem 原理
  - vue-config-js rootValue 换算基数 默认100
  - 如果个别地方不想转化px。可以简单的使用大写的 PX 或 Px 。
  - App.vue 中转换html的fontSize
  - 原理 使用rem 针对不同手机屏幕尺寸和dpr动态的改变根节点html的font-size大小(基准值)，再使用fis-postprocessor-px2rem插件让px自动转化成rem