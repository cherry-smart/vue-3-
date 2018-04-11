<template>
	<div class="seller" ref="ratings">
     <div class="seller-content">
     	<div class="overview">
     		<h1 class="title">{{seller.seller.name}}</h1>
     		<div class="desc">
     		 <star class="star":size="36" :score="seller.seller.score"></star>
     		 <span class="text">({{seller.seller.ratingCount}})</span>
     		 <span class="text">月售{{seller.seller.sellCount}}份</span>
     		</div>
     		<ul class="remark">
     			<li class="block">
     				<h2>起送价</h2>
     				<div class="content">
     					<span class="stress">{{seller.seller.minPrice}}</span>
     					元
     				</div>
     			</li>
     			<li class="block">
     				<h2>商家配送</h2>
     				<div class="content">
     					<span class="stress">{{seller.seller.deliveryPrice}}</span>
     					元
     				</div>
     			</li>
     			<li class="block">
     				<h2>平均配送时间</h2>
     				<div class="content">
     					<span class="stress">{{seller.seller.deliveryTime}}</span>
     					分钟
     				</div>
     			</li>
     			<div class="favorite">
     				<span class="icom-favorite" @click="togglefavorite">
     				    <img v-show="favorite==true" class="img" src="../../assets/love.png">
					  	<img v-show="favorite==false" class="img" src="../../assets/love1.png">
     				</span>
     				<span class="text">{{favoriteText}}</span>
     			</div>
     		</ul>
     	</div>
        <split></split>
        <div class="bulletin">
        	<h1 class="title">公告与活动</h1>
        	<div class="content-wrapper">
        		<p class="content">{{seller.seller.bulletin}}</p>
        	</div>
        </div>
        <div v-if="seller.seller.supports" class="supports">
						<li class="support-item" v-for="(item,key) in seller.seller.supports">
							<span class="icon" :class="classMap[item.type]"></span>
							<span class="text">{{item.description}}</span>
						</li>
		</div>
		 <split></split>
		 <div class="pics">
		 	<h1 class="title">商家实景</h1>
		 	<div class="pic-wrapper" ref="wrapper">	 		
		 		<ul class="pic-list" ref="pic-list" v-bind:style="styles">
		 			<li class="pic-item" v-for="pic in seller.seller.pics">
		 				<img :src="pic" width="120" height="90">
		 			</li>
		 		</ul>		
		 	</div>
		 </div>
         <split></split>
         <div class="info">
         	<div class="title">商家信息</div>
         		<ul>
         			<li class="info-item" v-for="item in seller.seller.infos">
         				{{item}}
         			</li>
         		</ul>       	
         </div>
     </div>

	</div>
</template>

<script>
	import BScroll from 'better-scroll';
	import {formatDate} from '../../common/js/formatdate';
	import split from '../split/split';
	import star from '../star/star';
	
	export default{
		props:{
			seller:{
				type:Object
			}
		},
		data(){
			return{
				styles:{
					width:'auto'
				},
				favorite:false
			}
			
		},
		computed:{
			favoriteText(){
				return this.favorite?'已收藏':'未收藏'
			}
		},
		created(){		
			
			if(this.seller.seller.pics){
				console.log("123");
						let picWidth=120;
						let margin=6;
						let width=(picWidth+margin)*this.seller.seller.pics.length-6;
						
						this.styles.width=width+"px";
					}
			this.classMap=['decrease','discount','special','invoice','guarantee']
		    this.$nextTick(() => {
					this.scroll = new BScroll(this.$refs.ratings, {
						click: true
					});	
					
					this.scroll = new BScroll(this.$refs.wrapper, {
						click: true,
						scrollX: true
					});		
			});
		},
		methods:{
			togglefavorite(){
				this.favorite=!this.favorite;
			}
			
		},
		components:{
			star,
			split
		}
	}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.seller
 position:absolute;
 top:174px;
 bottom:0px;
 left:0px;
 width:100%;
 overflow:hidden;
 .info
  padding:18px 18px 0 18px;
  color:rgb(7,17,27);
  text-align: left;
  .title
   padding-bottom:12px;
   line-height:18px;
   font-size:14px;
   border-bottom:1px solid rgba(7,17,27,0.1);
  .info-item
    padding:10px 12px;
    font-size:12px;
    line-height:16px;
    border-bottom:1px solid rgba(7,17,27,0.1);
    &:last-child
     border:none;
 .pics
  padding:18px;
  text-align:left;
  .pic-wrapper
   width:100%;
   overflow:hidden;
   white-space: nowrap;
   .pic-list
    font-size:0;
    .pic-item
     display:inline-block;
     margin-right:6px;
     width:120px;
     height:90px;
     &:last-child
      margin-right:0;     
  .title
   margin-bottom:8px;
   line-height:14px;
   font-size:14px;
   color:rgb(7,17,27);
 .supports
  padding:0px 18px;
  .support-item
   padding:16px 12px;
   font-size:0px;
   border-bottom:1px solid rgba(7,17,27,0.1);
   text-align: left;
   &:last-child
    border:none;
   .icon
   	display: inline-block;
   	width: 16px;
   	height:16px;
   	margin-right: 6px;
   	background-size: 16px 16px;
   	background-repeat: no-repeat;
   	vertical-align: top;
    &.decrease
     background-image:url('decrease_4@3x.png');
    &.discount
     background-image:url('discount_4@3x.png');
    &.special
     background-image:url('special_4@3x.png');
    &.invoice
     background-image:url('invoice_4@3x.png');
    &.guarantee
     background-image:url('guarantee_4@3x.png');
   .text
   	font-size: 12px;
   	line-height: 16px;
   	color:rgb(7,17,27);
   	margin: 0;
   	padding: 0;
 .bulletin
  padding: 18px 18px 0px 18px;
  text-align:left;
  .title
   margin-bottom:8px;
   line-height:14px;
   font-size:14px;
   color:rgb(7,17,27);
  .content-wrapper
    padding:0px 12px 16px 12px;
    border-bottom:1px solid rgba(7,17,27,0.1);
    .content
     line-height:24px;
     font-size:12px;
     color:rgb(240,20,20);
 .overview
  padding:18px;
  text-align:left;
  position:relative;
  .title
   margin-bottom:8px;
   line-height:14px;
   color:rgb(7,17,27);
   font-size: 14px;
  .desc
   padding-bottom:18px;
   border-bottom:1px solid rgba(7,17,27,0.1);
   font-size:0;
   .star
    display:inline-block;
    margin-right:8px;
    vertical-align:top;
   .text
    display:inline-block;
    margin-right:8px;
    line-height:18px;
    vertical-align:top;
    font-size:14px;
  .favorite
   position:absolute;
   right:18px;
   top:18px;
   z-index:10;
   text-align: center;
   .text
    font-size:10px;
    line-height:10px;
    color:#4B4848;
   .icom-favorite
    display:block;
    width:100%;
    height:24px;
    margin-bottom:4px;
    
    img
     text-align: center;
     width:24px;
     height:24px;
  .remark
   display: flex;
   padding-top:18px;
   .block
    flex:1;
    text-align:center;
    border-right:1px solid rgba(7,17,27,0.1);
    &:last-child
     border:none;
    h2
     margin-bottom:4px;
     line-height:10px;
     font-size:10px;
     color:rgb(147,153,159);
    .content
     line-height:24px;
     font-size:10px;
     color:rgb(7,17,27);
     .stress
      font-size:20px;
</style>