<template>
	<div class="cartcontrol">
		<transition enter-active-class="animated zoomIn" leave-active-class="animated zoomOut">
　　　　　      <div class="cart-decrease" v-show="food.count>0" @click="decreaseCart">
			        <img class="img" src="../../assets/decrease.png">
		     </div>
　　　　</transition>

		<div  class="cart-count" v-show="food.count>0">{{food.count}}</div>
		<div class="cart-add" @click="addCart">
			<img class="img" src="../../assets/add.png">
		</div>
	</div>

</template>

<script type="text/ecmascript-6">
	import Vue from 'vue';
export default {
	props: {
		food: {
			type: Object
		}
	},
	methods: {
		addCart() {
			if(!event._constructed) {
				return;
			}

			if(!this.food.count) {
				Vue.set(this.food, 'count', 1);
			} else {
				this.food.count++;
				let foodCount = this.food.count;
				Vue.delete(this.food, 'count');
				Vue.set(this.food, 'count', foodCount);

			}
		},
		decreaseCart(){
			if(!event._constructed) {
				return;
			}else {
				this.food.count--;
				let foodCount = this.food.count;
				Vue.delete(this.food, 'count');
				Vue.set(this.food, 'count', foodCount);

			}
		}

	}
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
 font-size:0;
 height:20px;
 margin:0;
 margin:0px;
 padding:0;
 .img
  width:20px;
  height:20px;
  border:none;
 .cart-decrease
  padding-top:6px;
  text-align:center;46650
  vertical-align: middle;
  float:left;
  width:24px;
  height:20px;
 .cart-count
  float:left;
  width:12px;
  padding-top:6px;
  line-height:20px;
  vertical-align: top;
  font-size:10px;
  color:rgb(147,153,159);
  text-align: center;
 .cart-add
  padding-top:6px;
  text-align:center;
  vertical-align: middle;
  float:left;
  width:24px;
  height:20px;

</style>
