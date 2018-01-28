<template>
  <div id="hello">
    <h1>{{ title }}{{msgFromFather}}</h1>
    <button v-on:click="onClickMe">Click Me!</button>
    <button v-on:click="onClickSay">儿子说</button>
  </div>
</template>

<script>
export default {
  /*name: 'App'*/

 data:function () {
    return {
      title: '我是你儿子',
    }
 },
 props:['msgFromFather'],//子组件必须要添加想听的内容，接收字符串的Key
/* events:{
 	 'onAddNew':function(items){
 	 	alert(items);
 	 }
 },*/
 methods:{
 	 onClickMe:function(){
 	 	 alert(this.msgFromFather);
 	 },
 	 onClickSay:function(){
 	 	 this.$emit('childTellme',this.title);
 	 	 //this.$dispatch('childTellme',this.title);
 	 }
 }

}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.finished{
	color: red;
	text-decoration: line-through;
}
</style>
