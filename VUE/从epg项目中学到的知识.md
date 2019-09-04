# 从epg项目中学到的知识

## axios安装与使用

### 安装

```bash
npm install axios --save ## 安装
```

### 修改api地址

在vue-cli中的的 **/config/index.js**中进行修改，主要配置 **proxyTable pathRewrite**

```javascript
// dev对象中
proxyTable: {
    '/api':{
        target: 'http://localhost:8080', // 目标地址
        changeOrigin: true, // 允许跨域
        pathRewrite: {
            '^/api' : "/static/mock/" // 表示把api 重定向到/static/mock
        }
    }
},
```

### 使用

在vue文件中我们首先要引文axios,然后发起请求啥的

```javascript
import axios from 'axios'
·······
// 获取数据
getHomeInfo () {
    axios.get('/api/data.json')
        .then(this.getHomeInfoSucc)
},
// 渲染数据
getHomeInfoSucc (res) {
  if (res.status == 200 && res.data) {
      const data = res.data;
      this.recommed1 = data.recommed1;
  }
},
```

也可以把axios配置在main.js中全局引用：

```javascript
import axios from 'axios'
Vue.prototype.$http = axios
```

