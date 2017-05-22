<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>欢迎来到我的vue世界,这里有你意想不到的精彩</h1>
    <h1 v-text='message'></h1>
    <h1 v-html='message'></h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <ul>
      <li v-for='item in items' v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinished(item)">{{item.label}}</li>
    </ul>
    <p>child tell me: {{childWords}}</p>
    <component-a dataFromfather='are you ok?'  v-on:child-tell-me-something='listenToMyBoy'></component-a>
    <!-- <router-view></router-view> -->
  </div>
</template>

<script>
// export default {
//   name: 'app'
// }
import storage from './components/storage.js'
import componentA from './components/componentA.vue'
export default {
  data:function(){
    return {
      message:'<span>??</span>this is a todo list',
      items:storage.fetch(),
      newItem:'',
      childWords:""
    }
  },
  components:{componentA},
   watch:{
    items:{
      handler:function(items){
          storage.save(items)
          console.log(items)
      },
      deep:true
    }
  },
  methods:{
    toggleFinished:function(item){
        item.isFinished=!item.isFinished;
    },
    addNew:function(){
        this.items.push({label:this.newItem,isFinished:true})
        this.newItem='';
    },
    listenToMyBoy:function(msg){
        this.childWords=msg;
    }
  }
 
}

</script>

<style>
.finished{
  text-decoration: underline;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
