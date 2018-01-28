<template>
  <div id="app">
    <!--<img src="./assets/logo.png"><br/>-->
   <!-- <router-view/>-->
    <h1>{{ title }}</h1>
    <input v-model="newItem" v-on:keyup.enter="addNewItem" />
    <!--<h1>{{ msg2 }}</h1>
    <h2 v-text="title"></h2>
    <h3 v-html="title2"></h3>-->
    <ul >
		  <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)"><!--[liClass1,liClass2]-->
		    {{ item.message }}
		  </li>
		</ul>
		<component-a msgFromFather='儿啊!' v-on:childTellme="listenToMySon"></component-a>
		<p>
			child tell me:{{childWords}}
		</p>
  </div>
</template>

<script>
import Store from  './store'//.js可以省略
import ComponentA from './components/componentA'
export default {
  /*name: 'App'*/
  components:{ComponentA},
data: function(){
 	return {
      title: 'This is todo list',
      title2: '<span>?</span>v-html会escape html标签',
      msg2: 'HelloWuqingvika',
      /*items: [
	      { message: 'eating' ,isFinished:true},
	      { message: 'coding',isFinished:false }
	    ],*/
	   items:Store.fetch() == null ? []: Store.fetch(),
	    liClass:"thisIsLiClass",
	    newItem:'',
	    childWords:''
    }
 },//这两种方法等价
/* data () {
    return {
      title: 'Welcome to Your Vue.js App',
      msg2: 'HelloWuqingvika'
    }
  }*/

 watch:{
 	 items:{
 	 	 handler:function(items){
 	 	 		//console.log(val,oldValue);
 	 	 		Store.save(items);
 	 	 },
 	 	 deep:true
 	 }
 },
 events:{
 	'childTellme':function(msg){
 		this.childWords=msg;
 	}
 },
 methods:{
 	toggleFinish: function(item){
 		item.isFinished=!item.isFinished;
 	},
 	addNewItem:function(){
 		this.items.push({
 			message:this.newItem,
 			isFinished:false
 		})
 		this.newItem='';
 		//this.$broadCast('onAddNew',this.items);
 	},
 	listenToMySon:function(msg){
 		this.childWords=msg;
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
