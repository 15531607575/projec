<template>
  <div class="listAllBox">
    <!-- <h1>{{ msg }}</h1> -->
	<div class="listBox" v-for="(item,index) in todeList" :key="index">
		<div v-if="item.status==1">{{item.name}}</div>
		<div v-if="item.status==2">
			<input :value="item.name" @input="handleInput($event,item)"/>
		</div>
		<div class="btnBox">
			<button class="btn" @click="del(index)">删除</button>
			<button class="btn" v-if="item.status==1" @click="edit(item)">修改</button>
			<button class="btn" v-if="item.status==2" @click="success(item)">保存</button>
		</div>
	</div>
  </div>
</template>

<script lang="ts" setup>
import { defineProps, defineEmits, toRefs } from 'vue';

const props = defineProps({
  todeList: Array
});

const { todeList } = toRefs(props);

const emit = defineEmits(['update-items']);

const del = (index: number) => {
  const newItems = [...todeList.value];
  newItems.splice(index, 1);
  emit('update-items', newItems);
};
const edit = (item: object) =>{
	item.status=2
}
function handleInput(event:any,item:object) {
	item.name=event.target.value
}
const success = (item: object) =>{
	item.status=1
	console.log(todeList)
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.listAllBox{
		width: 80vw;
		box-sizing: border-box;
		.listBox{
			width: 80vw;
			box-sizing: border-box;
			border:1px solid #ccc;
			padding: 20px;
			margin-bottom: 10px;
			.btnBox{
				margin-top: 20px;
				display: flex;
				align-items: center;
				.btn{
					margin-right: 10px;
				}
			}
		}
	}
	
</style>
