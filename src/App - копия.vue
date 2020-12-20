<template>
  <div class="t-head">Ты сегодня покормил кота?</div>
  <div class="content">
	<Gallery :menuSelector="menuSelector" :greetings="greetings" @select-pix="selectPix" @leave-pix="leavePix" @focus-pix="focusPix"/>
  </div>
</template>

<script>
//	SOURCE
//imgs paths
let paths = {
  defaultHover:	'defaultHover',
  selected:		'selected',
  selectedHover:'selectedHover',
  disabled_:	'kickIt/'
};
//input stock data
let fromBD = [
  {
    name:				'foie gras',
	pix:				'1.png',
	pixShortName:		'1',
	stockAvailability:	true
  },
  {
    name:				'with fish',
	pix:				'2.png',
	pixShortName:		'2',
	stockAvailability:	true
  },
  {
    name:				'with chicken',
	pix:				'3.png',
	pixShortName:		'3',
	stockAvailability:	false
	
  }
];
//
//let menuSelector	=	['1','2','disabled_/3'];
//
class Stock{
	constructor( data ){
		this.data 		= data;
		this.pixFormat	= '.png';
	}
	//Проверить на наличие товара
	checkAvailability( name ){
		//
		let shortName = name.indexOf('/') ? name.split('/')[name.split('/').length-1]+this.pixFormat : name+this.pixFormat;
		//
		let result = false;
		this.data.forEach( (element) => {result = (element.pix == shortName) ? element.stockAvailability : result} );
		console.log('stockAvailability '+name+' of: '+result);
		return result;
	}
	//
	checkAvailabilityAll( menuSelector ){
		this.data.forEach( (element) => {
			element.stockAvailability ? menuSelector.push(element.pixShortName) : menuSelector.push(paths.disabled_ + element.pixShortName)
		} );
	}
	//
}
//
let stock = new Stock( fromBD );
//


import Gallery from './components/Gallery.vue'

export default {
  name: 'App',
  components: {
    Gallery
  },
  
  data(){
	return {
		menuSelector: 	['1','2','kickIt/3'],
		greetings: 		['a','b','c'],
	}
  },
  
  methods: {
	selectPix( data ){
		if( stock.checkAvailability(data.pixName) ){
		//
			if( data.pixName.indexOf(paths.selectedHover) == -1 ){
				//
				this.menuSelector[ Number(data.index) ] = paths.selectedHover + '/' + data.pixName;
			}else{
				this.menuSelector[ Number(data.index) ] = data.pixName.split('/')[1];
			}
		}
		console.log( data );
	},
	focusPix( data ){
		if( stock.checkAvailability(data.pixName) ){
			if( (data.pixName.indexOf(paths.selectedHover) == -1) && (data.pixName.indexOf(paths.selected) > -1) ){
				//
				this.menuSelector[ Number(data.index) ] = paths.selectedHover + '/' + data.pixName.split('/')[1];
			}else{
				/*
				if( data.pixName.indexOf(paths.defaultHover) == -1) {
					this.menuSelector[ Number(data.index) ] = paths.defaultHover + '/' + data.pixName;
				}
				*/
			}
		}
	},
	leavePix( data ){
		if( stock.checkAvailability(data.pixName) ){
			if(data.pixName.indexOf(paths.selectedHover) > -1){
				this.menuSelector[ Number(data.index) ] = paths.selected + '/' + data.pixName.split('/')[1];
			}else{
				//this.menuSelector[ Number(data.index) ] = data.pixName.split('/')[1];
			}
		}
	}
  },
  
}
//
//stock.checkAvailabilityAll(menuSelector);
</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: 	center;
  margin-top: 	40px;
}

body {
	overflow: 			hidden;
	background-image: 	url("./assets/back.jpg");
	background-repeat:	repeat;
	
}

.t-head{
	font-family: 	Avenir, Helvetica, Arial, sans-serif;
	color: 			white;
	font-weight:	light;
	font-size:		20pt;
}

.content{
	display: block;
	flex-wrap: wrap;
	align-content: space-between;
	align-items: center;
	justify-content: center;
}
</style>
