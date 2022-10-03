Vue 上传文件
===

> Create by **jsliang** on **2019-3-21 16:57:58**  
> Recently revised in **2019-05-31 14:21:24**

## 一 设置 Node 跨域代理

修改 `项目/config/index.js` 下的 `dev` 设置：

> 原 build/index.js 配置：

```js
dev: {
  // Paths
  assetsSubDirectory: 'static',
  assetsPublicPath: '/',
  proxyTable: {},
}
```

> 修改后 build/index.js 配置：

```js
dev: {
  // Paths
  assetsSubDirectory: 'static',
  assetsPublicPath: '/',
  proxyTable: {
    '/services': { // 碰到 /services 类型的接口，使用 node 代理
      target: 'http://172.**.**.49:8080', // 需要将开发模式的 localhost:8080 代理到哪个接口
      changeOrigin: true, // 如果接口跨域，需要设置这个参数为 true
    }
  },
},
```

这时，我们在 `npm run dev` 下，就可以将 `localhost:8080` 调用 `http://172.**.**.49:8080` 的接口由 Node 代理转发，从而实现接口的跨域请求。

## 二 实现原生上传图片

> 章节 1 为前置条件

如何实现 `<input type="file" />` 上传图片：

> Album.vue

```html
<template>
  <div>
    <input type="file" @change="uploads">
  </div>
</template>

<script>
  // 如果使用方法 1
  // import { uploadFile } from '../../api/api'
  
  // 如果使用方法 2
  import axios from 'axios'
  
  export default {
    methods: {
      // 普通上传图片
      uploads(e) {

        // 方法 1 - 可行
        // const file = e.target.files[0];
        // console.log(file);
        
        // const fd = new FormData();
        // fd.append('userBlicence', file);

        // uploadFile(fd).then( res => {
        //   console.log(res);
        // }).catch( error => {
        //   console.log(error);
        // })

        // 方法 2 - 可行
        const file = e.target.files[0];
        console.log(file);
        
        const fd = new FormData();
        fd.append('userBlicence', file);

        axios({
          method: 'post',
          timeout: 5000,
          headers: {
            'Content-Type':'multipart/form-data',
            timestamp: "2019032009000",
            deviceid: "10001",
            signature: "2743cfbda4601a359400929393b7657a",
          },
          url: '/services/Auser-uploadImg.action',
          data: fd,
        }).then( res => {
          console.log(res);
        }).catch( error => {
          console.log(error);
        })

      },
    }
  }
</script>
```

如果我们不用封装接口，那么我们直接使用方法 2 即可。

但是，一般情况下，我们会抽取接口到 `api.js`，进行接口的统一管理：

> api.js

```js
// 设置 axios
import axios from 'axios';

// 请求配置
const request = axios.create({
  // 开发模式下不需要开启，打包模式下去掉该注释
  // baseURL: 'http://172.**.**.49:8080',
  timeout: 5000,
  headers: {
    timestamp: "2019032009000",
    deviceid: "10001",
    signature: "2743cfbda4601a359400929393b7657a",
  }
})

/**
 * 上传图片
 * userBlicence - 图片
 */
export const uploadFile = data => request({
  method: 'post',
  headers: {
    'Content-Type':'multipart/form-data',
  },
  url: '/services/Auser-uploadImg.action',
  data: data,
})
```

这样，当我们使用方法 1 的时候，我们直接调用接口即可。

## 三 实现 ElementUI 上传图片

> 章节 1 为前置条件

相对于原生上传图片来说，ElementUI 上传图片更为便捷：

```html

<template>
  <div>
    <el-upload
      action="/services/Auser-uploadImg.action"
      name="userBlicence"
      :on-success="uploadSuccess"
      :headers="headers"
    >
      <el-button type="primary">点击上传</el-button>
    </el-upload>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        headers: {
          timestamp: "2019032009000",
          deviceid: "10001",
          signature: "2743cfbda4601a359400929393b7657a",
        }
      }
    },
    methods: {
      // ElementUI 上传图片成功
      uploadSuccess(res, file) {
        console.log(res);
        console.log(file);
      },
    }
  }
</script>
```

如此，就可以实现图片上传的功能。

---



