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

## 7. this指向问题
  1、函数执行时首先看函数名前面是否有"."，有的话，"."前面是谁,this就是谁；没有的话this就是window

      function fn(){
        console.log(this);
      }
      var obj={fn:fn};
      fn();//this->window
      obj.fn();//this->obj
      function sum(){
          fn();//this->window
      }
      sum();
      var oo={
      sum:function(){
      console.log(this);//this->oo
            fn()；//this->window
        }
      };
      oo.sum();


  必须要注意一点：类中某一个属性值(方法)，方法中的this需要看方法执行的时候，前面是否有".",才能知道this是谁。

    function Fn(){
      this.x=100；//this->f1
      this.getX=function(){
      console.log(this.x);//this->需要看getX执行的时候才知道
        }
    }
    var f1=new Fn;
    f1.getX();//->方法中的this是f1，所以f1.x=100
    var ss=f1.getX;
    ss();//->方法中的this是window ->undefined
## 8.apply，call， bind 用法区别
    我们先来看一个问题，想在下面的例子中this绑定obj,怎么实现？

      var obj={name:"浪里行舟"};
      function fn(){
        console.log(this);//this=>window
      }
      fn();
      obj.fn();//->Uncaught TypeError:obj.fn is not a function

  #### 如果直接绑定obj.fn(),程序就会报错。这里我们应该用fn.call(obj)就可以实现this绑定obj,接下来我们详细介绍下call方法：

  #### call方法的作用:
  #### ①首先我们让原型上的call方法执行，在执行call方法的时候，我们让fn方法中的this变为第一个参数obj；然后再把fn这个函数执行。

  #### ②call还可以传值，在严格模式下和非严格模式下，得到值不一样。

    //在非严格模式下
    var obj={name:"浪里行舟 "};
    function fn(num1,num2){
      console.log(num1+num2);
      console.log(this);
    }
    fn.call(100,200);//this->100 num1=200 num2=undefined
    fn.call(obj,100,200);//this->obj num1=100 num2=200
    fn.call();//this->window
    fn.call(null);//this->window
    fn.call(undefined);//this->window

##

      //严格模式下 
      fn.call();//在严格模式下this->undefined
      fn.call(null);// 在严格模式 下this->null
      fn.call(undefined);//在严格模式下this->undefined
#### bind体现了预处理思想：事先把fn的this改变为我们想要的结果，并且把对应的参数值也准备好，以后要用到了，直接的执行即可

#### call和apply直接执行函数，而bind需要再一次调用。

    var a ={
          name : "Cherry",
          fn : function (a,b) {
              console.log( a + b)
          }
      }
    var b = a.fn;
    b.bind(a,1,2)
    // 如需执行函数 需要手动调用
    b.bind(a,1,2)()

## 9.箭头函数的this指向
现在，箭头函数完全修复了this的指向，**箭头函数没有自己的this，箭头函数的this不是调用的时候决定的，而是在定义的时候处在的对象就是它的this。**

换句话说，**箭头函数的this看外层的是否有函数，如果有，外层函数的this就是内部箭头函数的this，如果没有，则this是window。**

### 参考文章 

[你还没搞懂this?](https://segmentfault.com/a/1190000016680885)

[this、apply、call、bind++](https://juejin.im/post/59bfe84351882531b730bac2)

## 10.js在一个数组里随机选出不重复xx项?

	var result = [];
	var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14];
	
	var count = arr.length;
	for (var i = 0; i < 10; i++) {
	    var index = ~~(Math.random() * count) + i;
	    result[i] = arr[index];
	    arr[index] = arr[i];
	    count--;
	}
	
	console.log(result);
	
#
	算法简述：
	
	把源数组分成左右两段，左边按顺序递增，保存已选择的随机数；右侧是剩余可选的数值；
    从右侧选一个，与左	侧最后一个位置的数值交换就可以达到目的。
	
	然后考虑把左侧用一个新数组表示，右侧选中的数移入新数组，再将左侧应该交换过来的值移过来……
	
![avatar](https://bmsoft.oss-cn-shanghai.aliyuncs.com/images/4175043505-57cd8230d552b.png)
	
## 11.利用 a 标签解析 URL
  ##### 创建一个 a 标签将需要解析的 URL 赋值给 a 的 href 属性，然后我们就能很方便的拿到这些内容。代码如下：
         
    
    function parseURL(url) {
        var a =  document.createElement('a');
        a.href = url;
        return {
            host: a.hostname,
            port: a.port,
            query: a.search,
            params: (function(){
                var ret = {},
                    seg = a.search.replace(/^\?/,'').split('&'),
                    len = seg.length, i = 0, s;
                for (;i<len;i++) {
                    if (!seg[i]) { continue; }
                    s = seg[i].split('=');
                    ret[s[0]] = s[1];
                }
                return ret;
            })(),
            hash: a.hash.replace('#','')
        };
    }
	















      



