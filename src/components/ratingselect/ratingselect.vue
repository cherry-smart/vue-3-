<template>
	<div class="ratingselect">
		<div class="rating-type">
			<span @click="select(2,$event)" class="block positive":class="{'active':myselectType==2}">{{mydesc.all}}<span class="count">{{ratings.length}}</span></span>
			<span @click="select(0,$event)"  class="block positive" :class="{'active':myselectType==0}">{{mydesc.positive}}<span class="count"><!--{{ (ratings|positives).length}}-->2</span></span>
			<span @click="select(1,$event)"  class="block negative" :class="{'active':myselectType==1}">{{mydesc.negative}}<span class="count"><!--{{ ratings|negatives}}-->1</span></span>
		</div>
		<div class="switch" @click="toggleContent">
		  <span class="icon_true" :class="{'active':myonlyContent}"></span>
		  <span class="text">只看有内容的评价</span>
		</div>
	</div>
</template>

<script>
	import Vue from 'vue';
	
	
const POSITIVE = 0;
const NEGATIVE = 1;
const ALL = 2;
export default {
	props: {
		ratings: {
			type: Array,
			default() {
				return [];
			}
		},
		selectType: {
			type: Number,
			default: 2
		},
		onlyContent: {
			type: Boolean,
			default: false
		},
		desc: {
			type: Object,
			default() {
				return {
					all: '全部',
					positive: '满意',
					negative: '不满意'
				}
			}
		}
	},
	data() {
		return {
			myselectType: this.selectType,
			myonlyContent: this.onlyContent,
			mydesc: this.desc
		}
	},
	/*filters: {  
            positives(value){  
               //return this.rating.filter((ratings) => {
				return value.rateType == POSITIVE;
			  //});
            }  
        }, */ 
	/*computed: {
		positives() {
			return this.rating.filter((ratings) => {
				return rating.rateType == POSITIVE;
			});
		},
		negatives() {
			return this.rating.filter((ratings) => {
				return rating.rateType == NEGATIVE;
			});
		}

	},*/
	methods: {
		select(key, event) {
			if(!event._constructed) {
				return;
			} else {
				this.myselectType = key;
				//Vue.set(this.selectType,);
				//Vue.set(this.selectType,key);
				console.log(this.myselectType);
			}
		},
		
		toggleContent() {
			if(!event._constructed) {
				return;
			} else {
				this.myonlyContent = !this.myonlyContent;
			}
		}
	}
};
/*Vue.filter('positives',function(){
         return ratings.rateType == POSITIVE;
         return 3;

    });
    Vue.filter('negatives',function(){
         return ratings.rateType == NEGATIVE;

    });*/
</script>

<style lang="stylus" rel="stylesheet/stylus">
.ratingselect
 .rating-type
  padding:18px 0;
  margin:0 18px;
  border-bottom:1px solid rgba(7,17,27,0.1);
  font-size:0px;
  text-align:left;
  .block
   display: inline-block;
   padding:8px 12px;
   border-radius:1px;
   margin-right:8px;
   color:#fff;
   font-size:12px;
   color:rgb(77,85,93);
   line-height:16px;
   &.active
    color:#fff;
   .count
    font-size:8px;
    margin-left:2px;
   &.positive
    background:rgba(0,160,220,0.2);
    &.active
     background:rgb(0,160,220);
   &.negative
    background:rgba(77,85,93,0.2);
    &.active
     background:#4C4E50;
 .switch
  padding:12px 18px;
  color:rgb(147,153,159);
  line-height:24px;
  height:24px;
  border-bottom:1px solid rgba(7,17,27,0.1);
  font-size:0px;
  .text
   font-size:14px;
   float:left;
   display:inline-block;
  .icon_true  
   display:inline-block;
   float:left;
   width:24px;
   height:24px;
   line-height:24px;
   margin-right:10px;
   position:relative;
   border-radius: 50%;
   background:#CCCCCC;
   &.active
    background:#00c850;
  .icon_true:after
    content: "";
    position: absolute;
    left: 4px;
    bottom: 9px;
    width: 12px;
    height: 6px;
    border: 2px solid #fff;
    border-top-color: transparent;
    border-right-color: transparent;
    -ms-transform: rotate(-60deg);
    -moz-transform: rotate(-60deg);
    -webkit-transform: rotate(-60deg);
    transform: rotate(-45deg);
</style>