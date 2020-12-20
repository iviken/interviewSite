<template>
	<div class="t-head">Ты сегодня покормил кота?</div>
	<div class="content">
		<Gallery :menuSelector="menuSelector" @select-pix="selectPix" @leave-pix="leavePix" @focus-pix="focusPix"/>
	</div>
</template>

<script>
//	SOURCE
//imgs paths
let paths = {
	defaultHover:	'defaultHover/',
	selected:		'selected/',
	selectedHover:'selectedHover/',
	disabled_:	'kickIt/'
};
//input stock data
let fromBD = [
  {
    name:				'foie gras',
	pix:				'1.png',
	pixShortName:		'1',
	stockAvailability:	true,
	unclickText:		'Порадуй котейку) ',
	clickText:			'Печень утки разварная с артишрками.',
	endedText:			'Печалька, с фуа-гра закончился.'
  },
  {
    name:				'with fish',
	pix:				'2.png',
	pixShortName:		'2',
	stockAvailability:	true,
	unclickText:		'Чего сидишь? Порадуй катейку, ',
	clickText:			'Головы щучьи с чесноком, да свежайшая сёмгушка.',
	endedText:			'Печалька, с рыбой закончился.'
  },
  {
    name:				'with chicken',
	pix:				'3.png',
	pixShortName:		'3',
	stockAvailability:	false,
	unclickText:		'Чего сидишь? Порадуй катэ, ',
	clickText:			'Филе из цыплят с трюфелями в бульоне.',
	endedText:			'Печалька, с курой закончился.'
  }
];
//
class Card{
	constructor( cardIndex ){
		this.data 		= fromBD;
		this.cardIndex	= cardIndex;
		this.state		= 'unselect';
		this.paths		= paths;
		this.pixName	= fromBD[cardIndex].pix;
		this.currentPixName	= this.pixName;
		this.product	= this.data[cardIndex];
		this.flag_stateCheck	=	true;
		this.currentText='';
		this.textClass	=	{
			inStock: 'card-text_1',
			ended:	 'card-text_2'
		};
	}
	//
	setCurrentPix( eventIn ){
		if( this.product.stockAvailability ){
			this.flag_stateCheck = true;
			let SM =[
				['unselect', 'focus', this.paths.defaultHover+this.pixName, 'unselect'],
				['unselect', 'leave', this.pixName,							'unselect'],
				['unselect', 'select',this.paths.selectedHover + this.pixName, 'select'],
				['select',	 'focus', this.paths.selectedHover + this.pixName, 'select'],
				['select',	 'leave', this.paths.selected + 	this.pixName, 'select'],
				['select',	 'select',this.paths.defaultHover+this.pixName, 'unselect']
			];
			SM.forEach( (element, ch) => {
				if( (element[0] == this.state) && (element[1] == eventIn) && (this.flag_stateCheck) ){
					this.currentPixName = element[2];
					this.state			= element[3];
					this.flag_stateCheck= false;
					console.log (ch);
				}
			} );
			console.log(this.state+' '+eventIn);
			/*
			switch (eventIn){
				case 'select':
					if( this.state != 'select' ){
						
						this.state = 'select';
					};
				break;
				case 'focus':
					if( this.currentPixName != this.paths.selectedHover ){
						this.currentPixName = this.state == 'select' ? this.paths.selectedHover + this.product.pix : this.paths.defaultHover + this.product.pix;
					}
				break;
				case 'leave':
					
				break;
			}
			*/
		}
	}
	//
	getCurrentPix(){
		if( !this.product.stockAvailability ){
			this.state			=	'ended';
			this.currentPixName	=	this.paths.disabled_ + this.pixName;
		}
		return this.currentPixName;
	}
	//
	getText(){
		this.currentText = this.product.stockAvailability ? this.state == 'select' ? this.product.clickText : this.product.unclickText : this.product.endedText;
		return this.currentText;
	}
	//
	getTextClass(){
		return this.state == 'ended' ? this.textClass.ended : this.textClass.inStock;
	}
}
//
import Gallery from './components/Gallery.vue'

export default {
	name: 'App',
	components: {
		Gallery
	},
  
	data(){
		return {
			menuSelector: 	[ new Card(0), new Card(1), new Card(2) ],
		}
	},
  
	methods: {
		selectPix( data ){
			data.pixName.setCurrentPix('select');
		},
		focusPix( data ){
			data.pixName.setCurrentPix('focus');
		},
		leavePix( data ){
			data.pixName.setCurrentPix('leave');
		}
	},
  
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Jura:wght@300&display=swap');

#app {
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: 	center;
	margin-top: 	60px;
}

body {
	background-image: 	url("./assets/back.jpg");
	background-repeat:	repeat;
	
}
@media (min-width:	1024px){
	body {
		overflow: 		hidden;
	}
}

.t-head{
	font-family: 'Jura', sans-serif;
	color: 			white;
	font-weight:	light;
	font-size:		20pt;
}

.content{
	display: 		block;
	flex-wrap: 		wrap;
	align-content: 	space-between;
	align-items: 	center;
	justify-content:center;
}
</style>
