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

## 5.ruduce的高级用法
  ![avatar](https://bmsoft.oss-cn-shanghai.aliyuncs.com/images/reduce.png)

  https://segmentfault.com/a/1190000005921341 讲解reduce的精华帖




    reduce 支持两个参数 1 callback 2 initalValue
    -- 1 没有initalValue 
      那么callback 里的prev curr index arr 中prev 就是数组中的第一个，curr是第二个 index为1
    -- 2 有initalValue
    	那么callback 中的prev 为initalValue curr 为 数组第一项

      Note: 空数组没有initalValue 将会是一个error

## 6.代码的简洁之道

  通过 flag 的 true 或 false，来判断执行逻辑，违反了一个函数干一件事的原则。

  Bad:

    function createFile(name, temp) {
      if (temp) {
        fs.create(`./temp/${name}`);
      } else {
        fs.create(name);
      }
    }
    
  Good

    function createFile(name) {
      fs.create(name);
    }
    function createFileTemplate(name) {
      createFile(`./temp/${name}`)
    }   



















      



