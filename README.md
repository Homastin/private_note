#  homastin notes

## 1.wepy 手动封装promise ,wepy.request() try catch 失败问题 
    -- 解决办法
    app.wpy 加入 
      import 'wepy-async-function'
      constructor() {
        super();
        this.use('requestfix');
        // 使API promise化
        this.use('promisify');
      }

## 2.vue 项目使用axios
    -- 解决方法
    'Content-Type': 'application/x-www-form-urlencoded' 
        需要使用 Set 集合 或者引入 qs库，使用qs.stringify() 方法
    'Content-Type': 'application/x-www-form-urlencoded' 
      直接使用json

 ## 3.vue 项目使用proxytable   
  --- 解决方法

    proxyTable: {
      '/apis': {
        // 测试环境
        target: 'http://www.thenewstep.cn/',  // 接口域名
        changeOrigin: true,  //是否跨域
        pathRewrite: {
            '^/apis': ''   //需要rewrite重写的,
        }              
      }

      
## 4.git 初始化仓库 本地和远程
 ![avatar](https://bmsoft.oss-cn-shanghai.aliyuncs.com/images/gitlab.png)


