<template>
    <div id="header">
    	<h1>{{msg}}</h1>
    	<input  class="inputText" placeholder="what's your task?" v-model='newItem' @keyup.enter="addItem">
    	<!-- <div v-html="msg" v-if='isShow'></div> 
    	<div v-text="msg" v-show='isShow'></div> -->
    	<ul>
    		<li v-for='item in items'>
				{{item.label}}<button  @click="deleteItem(item)">{{delect}}</button>
    		</li>

    	</ul>
	</div>
</template>

<script>
	import Store from '../Store'
	// console.log(Store);
    export default {
		data(){
			return {
				msg:'Todo list',
				isShow:false,
				items:Store.fetch(),
				newItem:'',
				delect:'delect'
			}
		},
		watch:{
			items:{
				handler: function (items) {
					Store.save(items)
				},
	      		deep: false				
			}
		},
		methods:{
			addItem:function(){
				this.items.push({
					label:this.newItem
				})
				this.newItem=''
			},
			 deleteItem: function (item) {
		      let index = this.items.indexOf(item)
		      this.items.splice(index, 1)
		    }
		}
	}
</script>
<style>
*{
	margin: 0;
	padding: 0;
}
ul{
	list-style: none;
}
li{
	margin-bottom: 12px;
	 border-bottom: 1px solid #d2d2d2;
}
h1{
  text-align: center;

}
#header{
	width: 400px;
	margin: 0 auto;
	position: relative;

}
button{
	position: absolute;
	right: 0;
}
.inputText {
  width: 100%;
  height: 30px;
  border: none;
  border-bottom: 1px solid #ddd;
  font-size: 20px;
  margin: 15px auto;
}
</style>
