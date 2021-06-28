<template>
  <div class="users">
    <h1>{{ msg }}</h1>
    <!--添加信息-->
    <form v-on:submit="addUser">
      <input type="text" v-model="newUser.name" placeholder="Enter Name" />
      <input type="text" v-model="newUser.email" placeholder="Enter email" />
      <input type="submit" value="Submit" />
    </form>


   <!--展示信息 -->
    <!-- <ul>
      <li v-for="user in users">
        <input type="checkbox" class="toggle" v-model="user.contracted">
        <span :class="{contracted:user.contracted}">
            {{user.name}}:{{user.email}}
        <button v-on:click="deleteUser(user)">x</button>
        </span>
      </li>
    </ul> -->
    <!-- Vue swiper -->
    <div style="width: 500px;height: 600px;">
      <slider :pages="pages" :sliderinit="sliderinit">
        <div style="width: 500px;height: 200px;">{{pages.name}}</div>
      </slider>
    </div>
  </div>
</template>

<script>
  import slider from 'vue-concise-slider'// 引入slider组件
  export default {
    name: 'Users',
    data () {
      return {
        msg: 'Welcome to Your Vue.js App',
        newUser:{},
        pages:[
          {name:"Mir ai",email:"1101662275@qq.com",contracted:false},
          {name:"Mir li",email:"1101662275@193.com",contracted:false},
          {name:"Mir da",email:"1101662275@163.com",contracted:false},
          {name:"Mir ap",email:"1101662275@haho.com",contracted:false},
        ],
        //滑动配置[obj]
        sliderinit: {
          currentPage: 0,//当前页码
          thresholdDistance: 500,//滑动判定距离
          thresholdTime: 100,//滑动判定时间
          autoplay:1000,//自动滚动[ms]
          loop:true,//循环滚动
          direction:'vertical',//方向设置，垂直滚动
          infinite:1,//无限滚动前后遍历数
          slidesToScroll:1,//每次滑动项数
        }
      }
    },
    components: {
      slider
    },
    methods:{
      addUser:function (e) {
        e.preventDefault();
        this.users.push({
          name:this.newUser.name,
          email:this.newUser.email,
          contracted:false
        })
      },
      deleteUser:function (user) {
        this.users.splice(this.users.indexOf(user),1)
      }
    },
    // created:function(){
    //   this.$http.get("http://jsonplaceholder.typicode.com/").then(function (response ) {
    //     console.log(response)
    //     this.users=response.data;
    //   })
    // }
    created:function () {
      this.$http.get("http://jsonplaceholder.typicode.com/users").then( (response) => {
        // console.log(response)
        this.users=response.data;
        // this.users=response.body;
      })
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .contracted{
    text-decoration: line-through;
  }
</style>
