---
title: 编排系统PC前端项目架构
---

## 集运页面编排系统

### 一、项目地址
- [编排环境：PC的开发仓库](http://10.70.152.159:4960/base/common/canvas-manager-web)
  - 注：<br>
1、多个项目共用PC编排环境，使用同一个PC仓库，编排环境PC仓库目前包含系统、权益超市、权益领取，后续还会陆续新增其他站点。<br>
2、PC工程本地启动工程后（localhost）默认连的接口是沙箱环境。     

### 二、开发规范
- clone仓库：

  `git clone http://10.70.152.159:4960/base/common/canvas-manager-web.git`
  - 注：<br>
如上述无权限尝试：
git clone http://name:password@10.70.152.159:4960/base/common/canvas-manager-web
密码中的特殊字符需转义：例如：encodeURIComponent('@')<br/>
- 分支包含：master（部署生产）、 develop（部署沙箱和预发）、 个人分支（开发各自需求）。<br/>
- 新建自己的开发分支，格式：名字-时间-修改内容（wgq-20210129-swipper_modify）：在自己的分支中开发，完成开发后，不用打包，提交到个人分支并合并到develop分支，通知部署人员部署沙箱/预发。<br/>  
  - 注：<br>
1、部署人员：
系统侧：林勤、郑勤园<br>
2、组件开发命名规范、目录结构以及具体代码实现参考现有组件，新组件需先在各自站点的在线文档中做好统计，并在PC-组件管理-组件模板库新增相应组件（沙箱中新增一次，预发中新增一次：生产数据和预发保持一致，不用单独新增。组件模板中文名称不能重复，可加前缀，例如：权益领取_轮播图，后端名称的英文前缀需保持一致，以Comp结尾，例如：RightsGet-SwiperComp）<br>
3、PC开发仓库中组件结构目录为：src-views-components-项目名称-xxx，具体组件中包含img图片文件夹，edit.vue文件为页面编辑管理-编辑页面-右侧属性区域，index.vue为组件本身（H5使用的即是此文件）。<br>
4、业务站点文件夹分配（其余均为系统文件夹，业务侧开发人员不得修改，如有修改公共组件的需求，请联系系统侧人员以及产品经理进行评审）：<br>
      - 权益超市：<br>
         - src-utils<br>
         - src-api-rightsMarket<br>
         - src-views-components-rights <br>
      - 权益领取：<br>
         - src-utils<br>
         - src-api-rightsGet<br>
         - src-views-components-rightsGet

### 三、前端开发的公共组件及方法
 - **链接列表**
   - 调用方法：参考超市的【轮播图】组件
   - 目录：src-views-components-rights-swiper-edit.vue<br>
   - 代码示例：
   ```
   import LinkDataSourceConfig from "@/views/components/common/linkDataSourceConfig";

   <el-drawer title="链接列表" class="link-source" append-to-body :visible.sync="isShowDrawer" direction="rtl" size="60%" :wrapperClosable="false">
      <link-data-source-config
        :width="680"
        :height="280"
        :size="1024"
        v-model="comps[compId].goodsList"
        @onClosed="isShowDrawer = false"
      ></link-data-source-config>
   </el-drawer>
   ```
 - **图片上传**
   - 调用方法：参考超市的【文字链】组件
   - 目录：src-views-components-rights-notice-edit.vue
   - 说明：图片上传均统一使用图片库管理，沙箱无法正常显示，预发和生产正常显示部署到CDN的图片。
   - 代码示例：
  ```
   import ChooseImage from '@/views/components/common/chooseImage'

   <ChooseImage 
      :disabled="comps[compId].multiplex == '1'" @onSuccess="handleUploadSuccess" 
      @onReset="handleRemove" 
      :url="comps[compId].img" 
      :imgInfo="{width: 80, height: 30, size:2048}"
   ></ChooseImage>
  ```
 - **富文本**
   - 调用方法：参考超市的【富文本】组件
   - 目录：src-views-components-rights-richText-edit.vue
   - 代码示例：
   ```
   import Tinymce from '@/components/Tinymce'

   <Tinymce ref="textPop" menubar v-model="comps[compId].descInfo" :height="200" v-else></Tinymce>
   ```
 - **ajax请求方法**
    - 调用方法：参考超市的【权益领取】组件
    - 目录：src-views-components-rights-rightsGet-index.vue
    - 说明：业务接口，权益超市是在src-api-rightsMarket中，使用的是 /utils/marketRequest；权益领取在src-api-rightsGet中，使用 /utils/rightsGetRequest；
   - 代码示例：
   ```
   import { getRightsGetList } from "@/api/rightsMarket/rights"

   getRightsGetList().then((res) => {
      //业务代码
   });
   ```

### 四、环境部署和访问
 - localhost环境：
    编排环境：PC：http://localhost:9528/#/page/manage
 - 沙箱环境：
    编排环境：PC：https://sandbox.open.10086.cn/56341495/canvas-manager-web/#/page/manage
 - 预发环境：
    编排环境：PC：https://dev.coc.10086.cn/staging-coc3/canvas/canvas-manager-web/#/page/manage
 - 生产环境：
    编排环境：PC：https://dev.coc.10086.cn/coc3/canvas/canvas-manager-web/#/page/manage

   - 注：<br>
1、PC的沙箱环境账号密码：
账号：testuser
密码：testpassword
验证码：123456<br>
2、预发同生产账号需要单独向一室王冲（wangchongxs@chinamobile.com）申请。
