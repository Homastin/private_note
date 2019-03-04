###  01. Vue render 方法

    import Vue from 'vue'
    import App from './App.vue'

    var app = new Vue({
      el: '#app',
      // 这里的 h 是 createElement 方法
      render: h => h(App)
    })
