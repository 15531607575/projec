<template>
  <div class="home">
	<div class="inputBox">
		<input type="text" placeholder="请输入创建功能名称" v-model="name" class="inputStyle"/>
		<button @click="add">创建</button>
	</div>
    <HelloWorld @update-items="updateItems" :todeList="todeList"/>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref,reactive } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src

export default defineComponent({
  name: 'HomeView',
  components: {
    HelloWorld,
  },
  setup(){
	const name = ref('')
	const todeList = reactive([
		{
			name:"第一条",
			status:1
		},{
			name:"第二条",
			status:1
		},{
			name:"第三条",
			status:1
		}
	])
	function add(){
		if(name.value==''){
			alert("请先输入功能名称")
			return
		}else{
			todeList.push({
				'name':name.value,
				'status':1
			})
			name.value=''
		}
	}
	function updateItems(newItems: any){
		todeList.length = 0;
		Object.assign(todeList,newItems)
	}
	return {
		name,
		todeList,
		add,
		updateItems
	}
  }
});
</script>
<style lang="scss">
	.home{
		width: 100vw;
		display: flex;
		align-items: center;
		flex-direction: column;
		padding:20px;
		.inputBox{
			width: 80vw;
			border: 1px solid #ccc;
			padding: 20px;
			display: flex;
			justify-content: flex-start;
			box-sizing: border-box;
			margin-bottom: 20px;
			.inputStyle{
				margin-right: 20px;
			}
		}
	}
</style>
