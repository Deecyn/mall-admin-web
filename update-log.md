## 我的修改：

### 1.关于品牌 logo 图片的上传

将 src/views/pms/brand/components/BrandDetail.vue 中的 data() 函数（在第 76 行左右）进行了修改：

```vue
data() {
  return {
    brand:Object.assign({}, defaultBrand),
    rules: {
      name: [
        {required: true, message: '请输入品牌名称', trigger: 'blur'},
        {min: 2, max: 140, message: '长度在 2 到 140 个字符', trigger: 'blur'}
      ],
      logo: [
        // {required: true, message: '请输入品牌logo', trigger: 'blur'}
      ],
      sort: [
        {type: 'number', message: '排序必须为数字'}
      ],
    }
  }
}
```

即把 logo: [] 中的那一行注释掉了，这样可以不用上传 logo 图片了。

### 2.修改删除商品品牌时的 http 请求方法

将 src/api/brand.js 中的 deleteBrand() 函数（在第 35 行左右）进行了修改：

```javascript
export function deleteBrand(id) {
  return request({
    url:'/brand/delete/'+id,
    method:'post',
  })
}
```

将请求方法 method 由原来的 get 改成了 post。

### 删掉登录界面的「获取体验账号」按钮

在 `src/views/login/index.vue` 文件中的以下代码（约第 40 行）中，删除掉「获取体验账号」按钮的代码，如以下代码中的注释：

```vue
<el-form-item style="margin-bottom: 60px;text-align: center">
  <el-button style="width: 45%" type="primary" :loading="loading" @click.native.prevent="handleLogin">
    登录
  </el-button>
<!--
  <el-button style="width: 45%" type="primary" @click.native.prevent="handleTry">
    获取体验账号
  </el-button>
-->
</el-form-item>
```

在 template 标签的 div 中，删除「公众号二维码」相关的代码（约从第 48 行开始），如以下代码中的注释：

```vue
<div>
......

<img :src="login_center_bg" class="login-center-layout">
<!--
<el-dialog
  title="公众号二维码"
  :visible.sync="dialogVisible"
  :show-close="false"
  :center="true"
  width="30%">
  <div style="text-align: center">
    <span class="font-title-large"><span class="color-main font-extra-large">关注公众号</span>回复<span class="color-main font-extra-large">体验</span>获取体验账号</span>
    <br>
    <img src="http://macro-oss.oss-cn-shenzhen.aliyuncs.com/mall/banner/qrcode_for_macrozheng_258.jpg" width="160" height="160" style="margin-top: 10px">
  </div>
  <span slot="footer" class="dialog-footer">
<el-button type="primary" @click="dialogConfirm">确定</el-button>
  </span>
</el-dialog>
-->

</div>
```



### 删除掉主页的「广告」部分

在 `src/views/home/index.vue` 文件中，

在名为 app-container 的 div 中，删除掉名为 address-layout 的子 div，如下面代码中的注释（约从第 3 行开始）：

```vue
<div class="app-container">
<!--
<div class="address-layout">
  <el-row :gutter="20">
    <el-col :span="6">
      <div class="out-border">
        <div class="layout-title">后台项目</div>
        <div class="color-main address-content">
          <a href="https://github.com/macrozheng/mall">mall</a>
        </div>
      </div>
    </el-col>
    <el-col :span="6">
      <div class="out-border">
        <div class="layout-title">前端项目</div>
        <div class="color-main address-content">
          <a href="https://github.com/macrozheng/mall-admin-web">mall-admin-web</a>
        </div>
      </div>
    </el-col>
    <el-col :span="6">
      <div class="out-border">
        <div class="layout-title">学习教程</div>
        <div class="color-main address-content">
          <a href="https://github.com/macrozheng/mall-learning">mall-learning</a>
        </div>
      </div>
    </el-col>
  </el-row>
</div>  -->
<div class="total-layout">......</div>

    ......
</div>
```

在名为 total-layout 的 div 后面，删除名为 mine-layout 的 el-card，如下面代码的注释（约从第 64 行开始）：

```vue
<div class="total-layout">......</div>

<!--
<el-card class="mine-layout">
  <div style="text-align: center">
    <img width="150px" height="150px" src="http://macro-oss.oss-cn-shenzhen.aliyuncs.com/mall/banner/qrcode_for_macrozheng_258.jpg">
  </div>
  <div style="text-align: center">mall全套学习教程连载中！</div>
  <div style="text-align: center;margin-top: 5px"><span class="color-main">关注公号</span>，第一时间获取。</div>
</el-card> -->

<div class="un-handle-layout">......</div>
```

### 修改登录时的用户名校验

在 `src/utils/validate.js` 文件中，修改 isvalidUsername() 函数的代码，使任意用户名可以登录。如以下代码中的注释（约从第一行开始）：

```js
export function isvalidUsername(str) {
  /* 删除以下代码：
  const valid_map = ['admin', 'test']
  return valid_map.indexOf(str.trim()) >= 0
  */

    /* 添加这行代码 */
  return str.trim().length>=3
}
```

## 修改 OSS 文件上传路径

修改 `src/components/Upload` 下的 singleUpload.vue 和 multiUpload.vue 文件中的，data() 函数中的 ossUploadUrl 的值。
