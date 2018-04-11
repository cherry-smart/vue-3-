<template>
<div id="header" class="header">
	<div class="content-warper">
		<div class="avatar">
			<img width="64" height="64" :src="seller.seller.avatar" />
		</div>
		<div class="content">
			<div class="title">
				<span class="brand"></span>
				<span class="name">{{seller.seller.name}}</span>
			</div>
			<div class="description">
				{{seller.seller.description}}/{{seller.seller.deliveryTime}}分钟送达
			</div>
			<div v-if="seller.seller.supports" class="supports">
				<span class="icon" :class="classMap[seller.seller.supports[0].type]"></span>
				<span class="text">{{seller.seller.supports[0].description}}</span>
			</div>
		</div>
		<div v-if="seller.seller.supports" class="support-count" @click="showDetail">
			<span class="count">{{seller.seller.supports.length}}个</span>
			<i class="icon-keyboard_arrow_right">></i>
		</div>

	</div>
	<div class="bulletin-wrapper" @click="showDetail">
		<span class="bulletin-title"></span><span class="bulletin-text">{{seller.seller.bulletin}}</span>
		<i class="i">></i>
	</div>
	<div class="background">
		<img :src="seller.seller.avatar" />
	</div>
	<transition name="fade" type="animation">
		<div class="detail" v-show="detailshow">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h3 class="name">{{seller.seller.name}}</h3>
					<div class="star-wrapper">
						<star :size="48" :score="seller.seller.score"></star>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">优惠信息</div>
						<div class="line"></div>
					</div>
					<div v-if="seller.seller.supports" class="supports">
						<li class="support-item" v-for="(item,key) in seller.seller.supports">
							<span class="icon" :class="classMap[item.type]"></span>
							<span class="text">{{item.description}}</span>
						</li>
					</div>
					<div class="title">
						<div class="line"></div>
						<div class="text">商家公告</div>
						<div class="line"></div>
					</div>
					<div class="bullentin">
						<div class="content">{{seller.seller.bulletin}}</div>
					</div>

				</div>
			</div>
			<div class="detail-close" @click="hideDetail">
				<div class="close"></div>
			</div>
		</div>
	</transition>

</div>
</template>

<script type="">
	import star from '../star/star';
	export default{
		props:{
			seller:{
				type:Object
			}	
		},
		data(){
			return{
				detailshow:false
			}
		},
		created(){
			this.classMap=['decrease','discount','special','invoice','guarantee']
		},
		components : {
         star
       },
       methods:{
		  showDetail(){
		  	this.detailshow=true;
		  },
		  hideDetail(){
		  	this.detailshow=false;
		  }
		}
	}
</script>
<style>
	.bullentin{
		width:80%;
		margin:0 auto;
	   text-align:left;
	}
	.bullentin .content{
		padding:0px 12px;
		line-height:24px;
		font-size:12px;
	
		
	}
	  /*关闭按钮*/  
        .close {
        	width: 32px;
        	height: 32px;
        	position: relative;
        }
        
        .close:before,
        .close:after {
        	content: '';
        	position: absolute;
        	top: 50%;
        	margin-left: -16px;
        	width: 32px;
        	height: 3px;
        	background-color: #909499;
        	-webkit-transform: rotate(45deg);
        	transform: rotate(45deg);
        }
        
        .close:after {
        	-webkit-transform: rotate(-45deg);
        	transform: rotate(-45deg);
        }       
        .support-item .decrease {
        	background-image: url('decrease_2@2x.png');
        }     
        .support-item .discount {
        	background-image: url('discount_2@2x.png');
        }
        
        .support-item .special {
        	background-image: url('special_2@2x.png');
        }
        
        .support-item .invoice {
        	background-image: url('invoice_2@2x.png');
        }
        
        .support-item .guarantee {
        	background-image: url('guarantee_2@2x.png');
        }
        
        .support-item .text {
        	line-height: 16px;
        	font-size: 12px;
        }
           
</style>
<style lang="stylus" rel="stylesheet/stylus"> 
   .header
    overflow:hidden
    position:relative;
    color:#fff;
    background: rgba(7,17,27,0.5);
    .content-warper
      padding:24px 12px 18px 24px;
      font-size:0px;
      text-align:left;
      position:relative;
      .avatar
         display:inline-block;
         vertical-align: top;
         img
            border-radius:2px;
      .content
         display:inline-block;
         font-size:14px;
         margin-left:16px;
         .title
            margin:2px 0px 8px 0
            .brand
             width:30px;
             height:18px;
             vertical-align: top;
             display:inline-block;
             background-size:30px 16px; 
             background-repeat: no-repeat;
             background-image:url(brand@2x.png);
            .name
             margin-left:6px;
             font-size:16px;
             line-height:18px;
             font-weight:bold;
	     .description
	       margin-bottom: 10px;
	       line-height:12px;
	       font-size:12px;   
	     .supports
	      .icon
	       display:inline-block;
	       width:12px
	       height:12px
	       margin-right:4px
	       background-size:12px 12px;
	       background-repeat: no-repeat;  
	       vertical-align: top;
	      .decrease
	        background-image:url('decrease_2@2x.png');
	      .discount
	        background-image:url('discount_2@2x.png');
	      .special
	        background-image:url('special_2@2x.png');
	      .invoice
	        background-image:url('invoice_2@2x.png');    
	      .guarantee
	        background-image:url('guarantee_2@2x.png');    
	      .text 
	        font-size:10px;
	        line-height:12px;
	        margin:0;
	        padding:0;
	    .support-count
	      position:absolute;
	      bottom:18px;
	      right:12px;
	      padding:0 8px ;
	      height:24px;
	      line-height:24px;
	      border-radius:14px;
	      background:rgba(0,0,0,0.2);
	      text-align:center;
	     .count 
	       font-size:10px;
	     .icon-keyboard_arrow_right 
	       font-size:10px;
	       height:24px;
	       line-height:24px;
	       width:12px;
	       margin-left:2px;
	    .bulletin-wrapper
	      height:28px;
	      line-height:28px;
	      padding:0 22px 0 12px;
	      white-space: nowrap;
	      overflow:hidden;
	      text-overflow:ellipsis;
	      background: rgba(7,17,27,0.2);
	      position:relative;
	     .bulletin-title
	      vertical-align: top;
	      margin-top:8px;
	      display:inline-block;
	      width:22px;
	      height:12px;
	      background-image:url(bulletin@2x.png);
	      background-size:22px 12px;
	      background-repeat:no-repeat;
	     .bulletin-text
	      vertical-align: top;
	      font-size:10px;
	      margin:0px 4px
	     .i
	      position:absolute;
	      font-size:10px;
	      right:12px;
    .background
	     position:absolute;
	     top:0;
	     left:0;
	     width:100%;
	     height:100%;
	     z-index:-1;
	     filter: blur(10px);
	     img
	      width:100%;
	      height:100%;
	.detail
	 position:fixed;
	 z-index:100;
	 width:100%;
	 height:100%;
	 overflow:auto;
	 top:0;
	 left:0;
	 background: rgba(7,17,27,0.8);
	 &.fade-enter-active  
	  opacity:1;
	 &.fade-leave-active
	  opacity:0;
	 .detail-wrapper
	   min-height:100%;
	   margin:0;
	   padding:0;
	   width:100%;
	   overflow-x:hidden;
	  .detail-main
	     margin-top:64px;
	     padding-bottom:64px;
	     .name
	      line-height:16px;
	      text-align:center;
	      font-size:16px;
	      font-weight:700;
	     .star-wrapper
	      margin-top:18px;
	      padding:2px 0;
	      text-align:center;
	     .title
	       width:80%;
	       display:flex;
	       margin:30px auto 24px auto;
	       .line
	         flex:1;
	         position:relative;
	         top:-6px;
	         border-bottom:1px solid rgba(255,255,255,0.2);
	       .text
	         padding:0px 12px;
	         font-size:12px;
	         font-weight:700;
	     .supports
	      width:80%;
	      margin:0 auto;
	      text-align: left;
	      .support-item
	       padding:0 12px;
	       margin-bottom:12px;
	       font-size:0px;
	       &:last-child
	        margin-bottom:0;
	       .icon
	        display:inline-block;
	        width:16px;
	        height:16px;
	        vertical-align:top;
	        margin-right:6px;
	        background-size:16px 16px;
	        background-repeat:no-repeat;
	 .detail-close
	   position:relative;
	   width:32px;
	   height:32px;
	   margin:-64px auto 0 auto;
	   clear:both;
	   font-size:32px;      
</style>
