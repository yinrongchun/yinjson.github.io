<template>
  <div class="hello">
      <div>{{msg}}</div>
      <div>{{dataFromfather}}</div>
      <button v-on:click='onClickMe'>click!</button>
  </div>
</template>

<script>
export default {
  // name: 'hello',
  data:function () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  props:['dataFromfather'],
  methods:{
    onClickMe:function(){
      console.log(this.dataFromfather);
      this.$emit('child-tell-me-something',this.msg)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
div{
  color: red;
}
</style>
