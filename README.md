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
   -- 参考天赐
