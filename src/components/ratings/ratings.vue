<template>
	<div  class="ratings" ref="ratings">
		<div class="ratings-content ">
			<div class="overview">
				<div class="overview-left">
					<h1 class="score">{{seller.seller.score}}</h1>
					<div class="title">综合评分</div>
					<div class="rank">高于周边商家{{seller.seller.rankRate}}%</div>
				</div>
				<div class="overview-right">
					<div class="score-warpper">
						<span class="title">服务态度</span>
						<star class="star" :size="36" :score="seller.seller.serviceScore"></star>
						<span class="score">{{seller.seller.serviceScore}}</span>
					</div>
					<div class="score-warpper">
						<span class="title">商品评分</span>
						<star class="star" :size="36" :score="seller.seller.foodScore"></star>
						<span class="score">{{seller.seller.foodScore}}</span>
					</div>
					<div class="deliveryTime">
						<span class="title">送达时间</span>
						<span class="title2">{{seller.seller.deliveryTime}}分钟</span>
					</div>
				</div>
			</div>		
		<split></split>
			<ratingselect :ratings="ratings":desc="desc" :select-type="selectType" :only-content="onlyContent"></ratingselect>
		<div class="rating-wrapper2">
			<ul>
				<li v-for="rating in ratings" class="rating-wrapper">
					<div class="avatar"><img width="28px" height="28px":src="rating.avatar"></div>
					<div class="content">
						<h1 class="name">{{rating.username}}</h1>
						<div class="star-wrapper">
							<star class="star":size="24" :score="rating.score"></star>
							<span class="deliveryTime" v-show="rating.deliveryTime!=''" >{{rating.deliveryTime}}分钟</span>					
						</div>
						<p class="text">{{rating.text}}</p>
						<div class="recommend" v-show="recommend!=''">
							<span v-for="item in rating.recommend">
								<span class="item">{{item}}</span>
							</span>
							
						</div>
		    			<div class="time">{{rating.rateTime | formatDates}}</div>
					</div>
				</li>
			</ul>
		</div>
	 </div>
	</div>
</template>

<script>	
	import BScroll from 'better-scroll';
	import {formatDate} from '../../common/js/formatdate';
	
	import star from '../star/star';
	import split from '../split/split';
	import ratingselect from '../ratingselect/ratingselect';

   const ALL = 2;
   export default {
	 props: {
		seller: {
			type: Object
		}
	 },
	 components: {
		star,
		split,
		ratingselect
	  },
	   filters: {
        formatDates(time) {
            var date = new Date(time);
            return formatDate(date, 'yyyy-MM-dd hh:mm');
        }
    },
	  created(){
	  	this.$nextTick(() => {			
					this.scroll = new BScroll(this.$refs.ratings, {
						click: true
					});				
			});
	  },
	  data() {
		return {
			ratings: [{
					"username": "3******c",
					"rateTime": 1469281964000,
					"deliveryTime": 30,
					"score": 5,
					"rateType": 0,
					"text": "不错,粥很好喝,我经常吃这一家,非常赞,以后也会常来吃,强烈推荐.",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": [
						"南瓜粥",
						"皮蛋瘦肉粥",
						"扁豆焖面",
						"娃娃菜炖豆腐",
						"牛肉馅饼"
					]
				},
				{
					"username": "2******3",
					"rateTime": 1469271264000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"deliveryTime": "",
					"text": "服务态度不错",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": [
						"扁豆焖面"
					]
				},
				{
					"username": "3******b",
					"rateTime": 1469261964000,
					"score": 3,
					"rateType": 1,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "1******c",
					"rateTime": 1469261864000,
					"deliveryTime": 20,
					"score": 5,
					"rateType": 0,
					"text": "良心店铺",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "2******d",
					"rateTime": 1469251264000,
					"deliveryTime": 10,
					"score": 4,
					"rateType": 0,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "9******0",
					"rateTime": 1469241964000,
					"deliveryTime": 70,
					"score": 1,
					"rateType": 1,
					"text": "送货速度蜗牛一样",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "d******c",
					"rateTime": 1469231964000,
					"deliveryTime": 30,
					"score": 5,
					"rateType": 0,
					"text": "很喜欢的粥店",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "2******3",
					"rateTime": 1469221264000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "量给的还可以",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "3******8",
					"rateTime": 1469211964000,
					"deliveryTime": "",
					"score": 3,
					"rateType": 1,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "a******a",
					"rateTime": 1469201964000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "孩子喜欢吃这家",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": [
						"南瓜粥"
					]
				},
				{
					"username": "3******3",
					"rateTime": 1469191264000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "粥挺好吃的",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "t******b",
					"rateTime": 1469181964000,
					"deliveryTime": "",
					"score": 3,
					"rateType": 1,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "f******c",
					"rateTime": 1469171964000,
					"deliveryTime": 15,
					"score": 5,
					"rateType": 0,
					"text": "送货速度很快",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "k******3",
					"rateTime": 1469161264000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "u******b",
					"rateTime": 1469151964000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "下雨天给快递小哥点个赞",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "s******c",
					"rateTime": 1469141964000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "好",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "z******3",
					"rateTime": 1469131264000,
					"deliveryTime": "",
					"score": 5,
					"rateType": 0,
					"text": "吃了还想再吃",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "n******b",
					"rateTime": 1469121964000,
					"deliveryTime": "",
					"score": 3,
					"rateType": 1,
					"text": "发票开的不对",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "m******c",
					"rateTime": 1469111964000,
					"deliveryTime": 30,
					"score": 5,
					"rateType": 0,
					"text": "好吃",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "l******3",
					"rateTime": 1469101264000,
					"deliveryTime": 40,
					"score": 5,
					"rateType": 0,
					"text": "还不错吧",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "3******o",
					"rateTime": 1469091964000,
					"deliveryTime": "",
					"score": 2,
					"rateType": 1,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "3******p",
					"rateTime": 1469081964000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "很喜欢的粥",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "o******k",
					"rateTime": 1469071264000,
					"deliveryTime": "",
					"score": 5,
					"rateType": 0,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				},
				{
					"username": "k******b",
					"rateTime": 1469061964000,
					"deliveryTime": "",
					"score": 4,
					"rateType": 0,
					"text": "",
					"avatar": "http://static.galileo.xiaojukeji.com/static/tms/default_header.png",
					"recommend": []
				}
			],
			selectType: ALL,
			onlyContent: false
		}
	}
};</script>
<style>
	/*.rating-wrapper2{
		padding:12px 0px;
	}*/
</style>
<style lang="stylus" rel="stylesheet/stylus">
.ratings
 position:absolute;
 top:174px;
 bottom:0px;
 overflow: hidden;
 width:100%;
 
 .ratings-content
  width:100%;
  
  .rating-wrapper
   padding:12px 18px;
   display:flex;
   border-bottom:1px solid rgba(7,17,27,0.1);
   .avatar
    border-radius:50%;
    flex:0 0 28px;
    width:28px;
    margin-right:12px;
    img
      border-radius:50%;
   .content
     position: relative;
     flex:1;
     text-align: left;
     .name
      margin-bottom:4px;
      line-height:12px;
      font-size:10px;
      color:rgb(7,17,27);
     .star-wrapper
      margin-bottom:6px;
      font-size:0px;
      .star
       display:inline-block;
       margin-right:6px;
       vertical-align: top;
      .deliveryTime
        display:inline-block;
        vertical-align:top;
        font-size:12px;
        color:rgb(143,153,157);
     .text
      line-height:18px;
      color:rgb(7,17,27);
      font-size:12px;
      margin-bottom:8px;
     .recommend
       line-height:16px;
       font-size:0px;
       .item
        display: inline-block;
        margin:0 8px 4px 0;
        font-size:9px;
        padding:0 6px;
        border:1px solid rgba(7,17,27,0.1);
        border-radius:1px;
        color:rgb(147,153,159);
        background: #fff;
     .time
      position:absolute;
      top:0;
      right:0px;
      color:rgb(147,153,159);
      font-size:9px;
         
  .overview
   display:flex;
   padding:18px 0;
   .overview-left
    flex:0 0 137px;
    width:137px;
    border-right:1px solid rgba(7,17,27,0.1);
    padding-bottom: 6px 0;
    text-align:center;
    @media only screen and (max-width:320px)
     flex:0 0 120px;
     width:120px;
    .score
     margin-bottom:6px;
     line-height:28px;
     font-size:24px;
     color:rgb(255,153,0);
    .title
     margin-bottom:8px;
     font-size:12px;
     line-height:12px;
     color:rgb(7,17,27);   
    .rank
     font-size: 10px;
     color:rgb(147,153,159);
     line-height:10px;
   .overview-right
    flex:1;
    padding:6px 0 6px 24px;
    text-align: left;
    @media only screen and (max-width:320px)
      padding-left:6px
    .score-warpper
     margin-bottom:8px;
     font-size:0; 
     .title
      display:inline-block;
      line-height:18px;
      font-size:12px;
      color:rgb(7,17,27);
     .star
      display:inline-block;
      margin:0 12px;
      vertical-align:top;
     .score
      display:inline-block;
      vertical-align:top;
      font-size:12px;
      line-height:18px;
      color:rgb(255,153,0);
    .deliveryTime
     font-size:0;
     .title2
      font-size:12px;
      color:#93999f;
      margin-left:12px;
     .title
      display:inline-block;
      line-height:18px
      font-size:12px;
      color:rgb(7,17,27);
      
  
</style>