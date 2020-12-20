<template>
  <div class="hello board">
	<div v-for="(item, index) in menuSelector" :key="index" class="card transi">
		<img :src="require(`../assets/${item}.png`)" class="pix" @click="selectPix(item, index)" @mouseleave="leavePix(item, index)" @mouseover="focusPix(item, index)">
	</div>
  </div>
  <div v-for="(text, index) in greetings" :key="index" class="text">
	{{text}}
  </div>
</template>

<script>
export default {
  name: 'Gallery',
  props: [
	'menuSelector',
	'greetings'
  ],
  methods: {
	selectPix(pixName, index){
		this.$emit('select-pix', {pixName: pixName, index: index})
	},
	leavePix(pixName, index){
		this.$emit('leave-pix', {pixName: pixName, index: index})
	},
	focusPix(pixName, index){
		this.$emit('focus-pix', {pixName: pixName, index: index})
		
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

.text {
	color:	white;
}

/*
.pix {
	border: 2px solid #bbb;
	transition: 1s;
}

.pix:hover {
	border: 2px solid #444;
	transition: 1s;
}
*/

.text {
	font-size: smaller;
	padding: 10px;
}

.transi {
  animation-name: Appearance;
  animation-duration: 2s;
  animation-timing-function: cubic-bezier(.1,-.6,.2,0);
}

@-webkit-keyframes Appearance {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@-o-keyframes Appearance {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@-moz-keyframes Appearance {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

@keyframes Appearance {
  0% {opacity: 0;}
  100% {opacity: 1;}
}

</style>
