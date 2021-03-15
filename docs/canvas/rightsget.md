---
title: 权益领取H5前端项目架构
---

## 集运页面编排系统

### 编排系统的H5页面前端项目架构

##### src目录树
```
tree -I node_modules src -L 3 -I images

src
├── api
│   ├── comp_login.js
│   └── rights.js
├── assets
│   └── js
│       └── vconsole.min.js
├── components
├── mixins
│   └── sendDataMixin.js
├── store
│   └── index.js
├── utils
│   ├── authHelp.js
│   ├── cookies.js
│   ├── env.js
│   ├── filter.js
│   ├── format.js
│   ├── getIndex.js
│   ├── request.js
│   ├── requestCoc.js
│   ├── share.js
│   ├── uidlogin.js
│   └── utils.js
├── views
│   ├── common
│   │   ├── 404.vue
│   │   └── NetworkError.vue
│   ├── components
│   │   ├── pic
│   │   │   └── index.vue
│   │   ├── swiper
│   │   │   └── index.vue
│   │   └── index.js
│   └── rights
│       └── index.vue
├── App.vue
├── main.js
└── router.js
```


### 一、需求地址
- [需求文档](http://10.71.164.32:8090/pages/viewpage.action?pageId=15076787) 
- [进度计划表:（包含项目成员、组件开发负责人、项目规划、开发进度、问题记录及修复等）](https://docs.qq.com/sheet/DVW9XZk1zVVVTZlZF?tab=BB08J2) 

### 二、项目地址
- [编排环境：PC的开发仓库](http://10.70.152.159:4960/base/common/canvas-manager-web)
- [运行环境：H5的开发仓库](http://10.70.152.159:4960/front/business/rightsget-h5-canvas)   
  - 注：<br>
1、多个项目共用PC编排环境，使用同一个PC仓库，编排环境PC仓库目前包含系统、权益超市、权益领取，后续还会陆续新增其他站点。<br>
2、H5运行环境（H5仓库）根据不同站点有不同的开发仓库。<br>
3、PC/H5工程本地启动工程后（localhost）默认连的接口是沙箱环境。     

### 三、开发规范
- 1、clone仓库：

  `git clone http://10.70.152.159:4960/front/business/rightsget-h5-canvas.git`

  `git clone http://10.70.152.159:4960/base/common/canvas-manager-web.git`
  - 注：<br/>
如上述无权限尝试：
git clone http://name:password@10.70.152.159:4960/front/business/rightsget-h5-canvas
密码中的特殊字符需转义：例如：encodeURIComponent('@')<br/>
- 2、H5侧分支管理各业务团队自定<br/>
- 3、H5侧建议沙箱环境：通知部署人员部署；预发环境：通知部署人员协调运维部署。<br/>  
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
3、预发环境群里联系运维刘锟部署，生产环境上线当日填写[上线手册](https://docs.qq.com/sheet/DSnJFVFZwY0NMZEhE?newPad=1&newPadType=clone&tab=a1hp50)，生产H5打好包后先邮件发送运维部署CDN，部署完成CDN后再联系运维部署IT。<br/>
 - 4、本地localhost路径 http://localhost:8080/56341495/rightsget-h5-canvas/grey/hometest ，在PC编排环境中可点击页面地址查看对应url，其中grey为测发地址，online为正发地址。<br/>
 - 5、组件开发命名规范、目录结构以及具体代码实现参考现有组件，新组件需先在 https://docs.qq.com/sheet/DVW9XZk1zVVVTZlZF?tab=8p7yfp 中做好统计，并在PC中-组件管理-组件模板库新增相应组件（沙箱中新增一次，预发中新增一次：生产数据和预发保持一致，不用单独新增。组件模板中文名称不能重复，可加前缀，例如：权益领取_轮播图，后端名称的英文前缀需保持一致，以Comp结尾，例如：RightsGet-SwiperComp）<br/>
 - 6、PC开发仓库中组件结构目录为：src-views-components-rightsGet-xxx，具体组件中包含img图片文件夹，edit.vue文件为页面编辑管理-编辑页面-右侧属性区域，index.vue为组件本身（H5使用的即是此文件）；H5开发仓库组件结构目录为：src-views-components-xxx。
 - 7、在PC开发仓库中开发完成新组件后，把rightsget下的新加组件，复制到H5开发仓库的components下，删除edit.vue，启动H5项目测试是否有异常，投产前把使用到的图片邮件发给运维部署到CDN，H5中使用的图片和打包后的部署文件要求均为CDN。

### 四、环境部署和访问
 - 1、localhost环境：<br>
    编排环境：PC：http://localhost:9528/#/page/manage<br>
    运行环境：H5：http://localhost:8080/56341495/rightsget-h5-canvas/grey/hometest
 - 2、沙箱环境：<br>
    编排环境：PC：https://sandbox.open.10086.cn/56341495/canvas-manager-web/#/<br>
运行环境：H5：https://sandbox.open.10086.cn/56341495/rightsget-h5-canvas/grey/hometest
 - 3、预发环境：<br>
    编排环境：PC：https://dev.coc.10086.cn/staging-coc3/canvas/canvas-manager-web/#/<br>
运行环境：H5：https://dev.coc.10086.cn/staging-coc3/canvas/rightsget-h5-canvas/grey/hometest
 - 4、生产环境：<br>
    编排环境：PC：https://dev.coc.10086.cn/coc3/canvas/canvas-manager-web/#/<br>
    运行环境：H5：https://dev.coc.10086.cn/coc3/canvas/rightsget-h5-canvas/grey/hometest<br>
(grey测试用，online正式用)
   - 注：<br>
1、PC的沙箱环境账号密码：<br>
账号：testuser<br>
密码：testpassword<br>
验证码：123456<br>
2、https://dev.coc.10086.cn/staging-coc3/canvas/rightsget-h5-canvas/grey/home?debug=1 url后带debug=1则打开vconsole，方便调试。

### 五、测试流程
 - 1、localhost自测PC+H5
 - 2、沙箱环境自测PC+H5
 - 3、预发环境自测PC+H5
 - 4、产品组测试
 - 5、测试组测试

### 六、bug管理
 - [产品验收的bug列表](
https://docs.qq.com/sheet/DVW9XZk1zVVVTZlZF?tab=e9uzls)

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
