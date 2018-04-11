<template>
<transition enter-active-class="animated slideInRight" leave-active-class="animated fadeOut">
<div v-show="showFlag" class="food" ref="food">
           <div>
		<div class="food-content" >
			<div class="image-header" @click="hide">
				<img :src="food.image">
				<span class="close"></span>
			</div>
		</div>
		<div class="content2" > 
			<div class="title">{{food.name}}</div>
			<div class="detail2">
				<span class="sell-count">月售{{food.sellCount}}份</span>
				<span class="rating">好评{{food.rating}}%</span>
			</div>
			<div class="price">
				<span class="now">¥{{food.price}}</span>
				<span class="old" v-show="food.oldPrice">¥{{food.oldPrice}}</span>
			</div>
			<div class="cartcontrol2" v-show="food.count>0">
				<cartcontral :food="food"></cartcontral>
			</div>
			<div class="buy" v-show="!food.count||food.count===0" @click="byy">加入购物车</div>
		</div>
		<split v-show="food.info"></split>
		<div class="info" v-show="food.info">
			<div class="title">商品信息</div>
			<div class="text">{{food.info}}</div>
		</div>
		<split></split>
		<div class="rating">
			<h1 class="title">商品评价</h1>
			<ratingselect :ratings="food.ratings":desc="desc" :select-type="selectType" :only-content="onlyContent"></ratingselect>
		    <div class="rating-wrapper">
		    	<ul class="" v-show="food.ratings && food.ratings.length">
		    		<li v-show="needshow(rating.rateType,rating.text)" v-for="rating in food.ratings"  class="rating-item">
		    			<div class="user">
		    				<span class="name">{{rating.username}}</span>
		    				<img class="avatar" width="12" height="12":src="rating.avatar">
		    			</div>
		    			<div class="time">{{rating.rateTime | formatDates}}</div>
		    			<p class="text">
		    				{{rating.text}}
		    			</p>
		    		</li>
		    	</ul>
		    	<div class="no-rating" v-show="!food.ratings || !food.ratings.length">
		     	               暂无评价
		    	</div>
		    </div>
		</div>
	</div>
	</div>
</transition>
</template>
<script>
	import BScroll from 'better-scroll';
	import Vue from 'vue';
	import {formatDate} from '../../common/js/formatdate';
	import cartcontral from '../cartcontral/cartcontral';
	import split from '../split/split';
	import ratingselect from '../ratingselect/ratingselect';

   const POSITIVE=0;
	const NEGATIVE=1;
	const ALL=2;
export default {
	props: {
		food: {
			type: Object
		}
	},
	data() {
		return {
			showFlag: false,
			selectType:ALL,
			onlyContent:false,
			desc:{
				all:'全部',
				positive:'推荐',
				negative:'吐槽'
			}
		};
	},
	methods: {
		show() {
			this.showFlag = true;
			this.selectType=ALL;
			this.onlyContent=true;
			this.$nextTick(() => {
				if(!this.scroll) {
					this.scroll = new BScroll(this.$refs.food, {
						click: true,
						scrollY: true
					});
				} else {
					this.scroll.refresh();
				}
			});
		},
		hide() {
			this.showFlag = false;
		},
		byy() {
			if(!event._constructed) {
				return;
			} 
			Vue.set(this.food, 'count', 1);
		},
		needshow(type,text){
			/*if(this.onlyContent&&!text){
				return false;
			}
			else if(this.onlyContent&&!text===ALL){
				return true;
			}
			else{
				return type=this.selectType;
			}*/
			return true;
		}
	},
	 filters: {
        formatDates(time) {
            var date = new Date(time);
            return formatDate(date, 'yyyy-MM-dd hh:mm');
        }
    },
	components: {
		'cartcontral': cartcontral,
		'split': split,
		'ratingselect':ratingselect
		}
	}
</script>
<style>
.food-content .image-header .close {
	width: 20px;
	height: 20px;
	position: absolute;
	top:16px;
	left:36px;
	border-radius:50%;
}
.food-content .image-header .close:before,
.food-content .image-header .close:after {
	content: '';
	position: absolute;
	top: 50%;
	width: 20px;
	height: 2px;
	background-color: #fff;
	-webkit-transform: rotate(45deg);
	transform: rotate(45deg);
}
.food-content .image-header .close:after {
	-webkit-transform: rotate(-45deg);
	transform: rotate(-45deg);
}
</style>
<style lang="stylus" rel="stylesheet/stylus">
.food
 position:fixed;
 left:0;
 top:0;
 bottom:48px;
 z-index: 30;
 width:100%;
 text-align: left;
 background: #fff;
 overflow:hidden;
 .food-content
  .image-header
   position:relative;
   width:100%;
   height:0;
   padding-top:100%;
   img
    position:absolute;
    left:0;
    top:0;
    width:100%;
    height:100%;
 .content2
    padding:18px;
    position:relative;
  .title
     line-height:14px;
     margin-bottom:8px;
     font-size:14px;
     font-weight:700;
     color:rgb(7,17,27);
  .detail2
     margin-bottom: 18px;
     line-height:10px;
     font-size:0;
     line-height: 10px;
    .sell-count,.rating
      font-size:10px;
      color:rgb(147,153,159);
    .rating
     margin-left:10px;
  .price
      display:inline-block;
      font-weight:700;
      line-height:24px;
    .now
       font-size:8px;
       margin-right:8px;
       color:rgb(240,20,20);
    .old
       text-decoration: line-through;
       font-size:10px;
       color:rgb(147,153,159);
   .cartcontrol2
    position:absolute;
    right:12px;
    bottom:18px;
   .buy
    position:absolute;
    right:18px;
    bottom:18px;
    z-index:10;
    height:24px;
    line-height:24px;
    padding:0 12px;
    box-sizing: border-box;
    font-size:10px;;
    border-radius:12px;
    color:#fff;
    background:rgb(0,160,220);
 .info
  padding:18px;
  .title
   line-height:14px;
   margin-bottom:6px;
   font-size:16px;
   color:rgb(7,17,27);
  .text
   line-height:27px;
   padding:0 8px;
   font-size:12px;
   color:#090909;
 .rating
  padding-top:18px;
  .title
   line-height:14px;
   margin-left:18px;
   font-size:16px;
   color:rgb(7,17,27); 
  .rating-wrapper
   .no-rating
    padding:16px 0;
    font-size:12px;
    color:rgb(147,153,159);
   padding:0 18px;
   .rating-item
    position:relative;
    padding:16px 0;
    border-bottom: 1px solid rgba(7,17,27,0.1);
    .text
     line-height:16px;
     font-size:12px;
     color:rgb(7,17,27);
    .time
     line-height:12px;
     font-size:10px;
     color:rgb(147,153,159);
     margin-bottom:6px;
    .user
     position:absolute;
     right:0px;
     top:16px;
     font-size:0px;
     line-height:12px;
     .name
      font-size:10px;
      display:inline-block;
      vertical-align:top;
      color:rgb(147,153,159);
      margin-right:6px;
     .avatar
      display:inline-block;
      border-radius:50%;
     
</style>