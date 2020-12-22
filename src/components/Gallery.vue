<template>
	<div class="gallery">
		<div class="t-head">Ты сегодня покормил кота?</div>
		<div class="hello board">
			<div v-for="(item, index) in menuSelector" :key="index" class="card transi">
				<img :src="require(`../assets/${item.getCurrentPix()}`)" class="pix" @click="selectPix(item)" @mouseleave="leavePix(item)" @mouseover="focusPix(item)">
				<div :class="item.getTextClass()">
					<small>
					{{item.getText()}}<a class="card-text_3" href="#" @click="selectPix(item)">{{item.getBuyText()}}</a>
					</small>
				</div>
			</div>
		</div>
		<div></div>
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
.t-head{
	font-family: 	'Jura', sans-serif;
	color: 			white;
	font-weight:	light;
	font-size:		20pt;
	padding:		40px 10px 0px 10px;
}

.gallery {
	display:		flex;
	flex-direction:	column;
	height:			100%;
}
/*
.gallery>div {
	border:			2px solid green;
}
*/
.gallery>div:nth-child(1) {
	
}

.board {
	display: 		flex;
	flex-wrap: 		wrap;
	align-content: 	space-between;
	align-items: 	center;
	justify-content:center;
	padding:		30px;	
}

.card {
	padding: 		20px;
}

.pix {
	width:			40vh;
}

.card-text_1 {
	color:			white;
	font-family:	Trebuchet MS;
	font-size:		smaller;
}
.card-text_2 {
	color:			yellow;
	font-family:	Trebuchet MS;
	font-size:		smaller;
}
.card-text_3 {
	color:			#1698d9;
	font-family:	Trebuchet MS;
	font-size:		smaller;
}
/*	For PC	*/

@media (min-width:	1600px){
	t-head {
		font-size:	xx-large;
	}
/*
	.card-text_2, card-text_2, card-text_3 {
		font-size:	smaller;
	}
*/
}



</style>
