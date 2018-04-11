<template>
<div>
	<div class="shopcart">
		<div class="content">
			<div class="content-left" @click="toggleList">
				<div class="logo-wrapper">
					<div class="logo" :class="{'hightlight':totalCount>0}">
						<span class="icon-shoping_cart">
					  	<img v-show="totalCount==0" class="img" src="../../assets/cart.png">
					  	<img v-show="totalCount>0" class="img" src="../../assets/cartf.png">
					  </span>
					</div>
					<div class="num" v-show="totalCount>0">{{totalCount}}</div>
				</div>
				<div class="price" :class="{'highlight':totalPrice>0}">￥{{totalPrice}}</div>
				<div class="desc">另需配送费￥{{deliveryprice}}块钱</div>
			</div>
			<div class="conetent-right" :class="payClass" @click="pay">
				{{payDesc}}
			</div>
		</div>
		<transition enter-active-class="animated slideInUp" leave-active-class="animated slideOutDown">
			<div class="shopcart-list" v-show="listshow">
				<div class="list-header">
					<h1 class="title">购物车</h1>
					<span class="empy" @click="empty">清空</span>
				</div>
				<div class="list-content" ref="listcontent">
					<ul>
						<li class="food" v-for="food in selectFoods">
							<span class="name">{{food.name}}</span>
							<div class="price">
								<span>￥{{food.price*food.count}}</span>
							</div>
							<div class="cartron-wrapper">
								<cartcontral :food="food"></cartcontral>
							</div>
						</li>
					</ul>
				</div>
			</div>
		</transition>
	</div>
	<div class="list-mask" v-show="listshow" @click="hideList">
	</div>
</div>
</template>

<script type="text/ecmascript-6">
	
	import BScroll from 'better-scroll'
	import cartcontral from '../cartcontral/cartcontral';

export default {
	props: {
		selectFoods: {
			type: Array,
			default() {
				return [{
					price: 10,
					count: 3
				}];
			}
		},
		deliveryprice: {
			type: Number,
			default: 0
		},
		minprice: {
			type: Number,
			default: 0
		}
	},
	data() {
		return {
			fold: true
		}
	},
	computed: {
		totalPrice() {
			let total = 0;
			this.selectFoods.forEach((food) => {
				total += food.price * food.count;
			});
			return total;
		},
		totalCount() {
			let count = 0;
			this.selectFoods.forEach((food) => {
				count += food.count;
			});
			return count;
		},
		payDesc() {
			if(this.totalPrice === 0) {
				return '￥' + this.minprice;
			} else if(this.totalPrice < this.minprice) {
				let diff = this.minprice - this.totalPrice;
				return '还差￥' + diff + '元起送';
			} else {
				return '去结算';
			}
		},
		payClass() {
			if(this.totalPrice < this.minprice) {
				return 'not-enough';
			} else {
				return 'enough';
			}
		},
		listshow() {
			if(!this.totalCount) {
				this.fold = true;
				return false;
			}
			let show = !this.fold;
			if(show) {
				if(!this.scroll){
					this.$nextTick(() => {
					this.scroll = new BScroll(this.$refs.listcontent, {
						click: true
					});
				});
				}else{
					this.scroll.refresh();
				}
				
			}

			return show;
		}
	},
	methods: {
		toggleList() {
			if(!this.totalCount) {
				return;
			} //console.log("123");
			this.fold = !this.fold;
		},
		empty(){
			this.selectFoods.forEach((food) =>{
				food.count=0;
			});
		},
		hideList(){
			this.fold = true;
		},
		pay(){
			if(this.totalPrice<this.minPrice){
				return;
			}window.alert("支付"+this.totalPrice);
		}
	},
	components: {
		'cartcontral': cartcontral
	}
};</script>
<style>
	.animated {
	animation-duration: 0.8s ease;
	animation-fill-mode: both
}
</style>
<style lang="stylus" rel="stylesheet/stylus">
.shopcart
 position:fixed;
 left:0px;
 bottom:0px;
 z-index:50;
 width:100%;
 height:48px;
 .content
   display:flex;
   background:#141d27;
   text-align: left;
   .content-left
    flex:1;
    .logo-wrapper
      float:left;
      position:relative;
      top:-10px;
      margin:0px 12px;
      padding: 6px;
      width:56px;
      height:56px;
      box-sizing: border-box;
      vertical-align: top;
      border-radius:50%;
      background:#141d27;
      font-size:0;
      .logo
       width:100%;
       height:100%;
       border-radius:50%;
       background: #2b343c;
       &.hightlight
         background: rgb(0,160,220);
       .icon-shoping_cart
        width:22px;
        height:22px;
        display:block;
        line-height:44px;
        color:#80858a;
        &.hightlight
         background: rgb(0,160,220);
        .img
          width:26px;
          height:26px;
          margin-left:9px;
          margin-top:9px;  
      .num
        position: absolute;
        top:0px;
        right:0px;
        width:24px;
        height: 16px;
        line-height:16px;
        text-align: center;
        border-radius:16px;
        font-size:9px;
        font-weight:700;
        background:rgb(240,20,20);
        color:#fff;
        box-shadow: 0 4px 8px rgba(0,0,0,0.4);
            
    .price
      float:left;
      vertical-align:top;
      line-height: 24px;
      margin-top:12px;
      border-right:1px solid rgba(255,255,255,0.1);
      box-sizing:border-box;
      padding-right:12px;
      font-size:16px;
      font-weight:700;
      color:rgba(255,255,255,0.1);
      &.highlight
       color:#fff;      
    .desc
      float:left;
      vertical-align:top;
      line-height:24px;
      margin-left:12px;
      margin-top:12px;
      color:#85878a;
      font-size:13px;  
   .conetent-right
    flex:0 0 105px;
    width:105px;
    background: ;
    height:48px;
    text-align: center;
    line-height:48px;
    color:#979a9c;
    font-size:12px;
    font-weight: 700;
    &.not_enough
     background:#2b333b;
    &.enough
     background:#00b43c;
     color:#fff;
 .ball-container
  .ball
   position:fixed;
   left:32px;
   bottom:22px;
   z-index:200;
   &.drop-transition
    transition:all 0.4s;
    .inner
      width:16px;
      height:16px;
      border-radius:50%;
      background:rgb(0,160,220);
 .shopcart-list
  position:absolute;
  left:0px;
  z-index:-1;
  bottom:48px;
  width:100%;
  .list-header
   height:40px;
   line-height:40px;
   padding:0 18px;
   background: #f3f5f7;
   border-bottom:1px solid rgba(7,17,27,0.1);
   .title
    float:left;
    font-size:14px;
    color:rgb(7,17,27);
   .empy
    float:right;
    color:rgb(0,160,220);
  .list-content
   padding:0 18px;
   max-height:217px; 
   background: #fff;
   overflow:auto;
   .food
    position:relative;
    padding:12px 0;
    text-align: left;
    border-bottom:1px solid rgba(7,17,27,0.1);
    box-sizing:border-box;
    .name
      text-align: left;
      line-height:24px;
      font-size:14px;
      color:rgb(7,17,27);
    .price
       position:absolute;
       right:90px;
       bottom:12px;
       line-height:24px;
       font-size:14px;
       font-weight:700;
       color:rgb(240,20,20);
    .cartron-wrapper
        position:absolute;
        right:0px;
        bottom:16px;       
.list-mask
 position:fixed;
 top:0;
 left:0;
 width:100%;
 height:100%;
 z-index:40;
 background:rgba(7,17,27,0.6);      
</style>