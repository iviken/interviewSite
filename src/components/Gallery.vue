<template>
  <div class="hello board">
	<div v-for="(item, index) in menuSelector" :key="index" class="card transi">
		<img :src="require(`../assets/${item.getCurrentPix()}`)" class="pix" @click="selectPix(item)" @mouseleave="leavePix(item)" @mouseover="focusPix(item)">
		<div :class="item.getTextClass()">
			<small>
			{{item.getText()}}
			</small>
		</div>
	</div>
  </div>
</template>

<script>
export default {
	name: 'Gallery',
	props: [
		'menuSelector',
	],
	methods: {
		selectPix(pixName){
			this.$emit('select-pix', {pixName: pixName})
		},
		leavePix(pixName){
			this.$emit('leave-pix', {pixName: pixName})
		},
		focusPix(pixName){
			this.$emit('focus-pix', {pixName: pixName})
			
		}
	},
}
</script>


<style scoped>

.board {
	display: flex;
	flex-wrap: wrap;
	align-content: space-between;
	padding: 40px;
	align-items: center;
	justify-content: center;
}

.card {
	padding: 15px;
}

.pix {
	width: 90%;
}

.card-text_1 {
	color:			white;
	font-family:	Trebuchet MS
}
.card-text_2 {
	color:	yellow;
	font-family:	Trebuchet MS
}





</style>
