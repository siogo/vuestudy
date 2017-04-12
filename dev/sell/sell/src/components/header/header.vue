<template>
	<div class="header topheader">
		<div class="content-wrapper">
			<div class="avatar">
				<img width="64" height="64" :src="seller.avatar">
			</div>
			<div class="content">
				<div class="title">
					<span class="brand"></span>
					<span class="name">{{seller.name}}</span>
				</div>
				<div class="description">
					{{seller.description}}/{{seller.deliveryTime}}分钟送达
				</div>
				<div v-if="seller.supports" class="support">
					<span class="icon" :class="classMap[seller.supports[0].type]"></span>
					<span class="text">{{seller.supports[0].description}}</span>
				</div>
			</div>
			<div v-if="seller.supports" class="support-count" @click="showDetail">
				<span class="count">{{seller.supports.length}}个</span>
				<i class="icon-keyboard_arrow_right"></i>
			</div>
		</div>
		<div class="bulletin-wrapper" @click="showDetail">
			<span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
			<i class="icon-keyboard_arrow_right"></i>
		</div>
		<div class="background">
			<img :src="seller.avatar" width="100%" height="100%">
		</div>
		<div v-show="detailshow" class="detail">
			<div class="detail-wrapper clearfix">
				<div class="detail-main">
					<h1 class="name">{{seller.name}}</h1>
					<star :size="48" :score="seller.score"></star>
				</div>
			</div>
			<div class="detail-close">
				<i class="icon-close"></i>
			</div>
		</div>
	</div>
</template>

<script type="text/ecmascript-6">
	import star from '../star/star.vue';

	export default{
		props:{
			seller:{
				type: Object
			}
		},
		data(){
			return {
				detailshow: false
			}
		},
		methods:{
			showDetail(){
				this.detailshow = true;
			}
		},
		created(){
			this.classMap = ['decrease','discount','special','invoice','guarantee']
		},
		components:{
			star
		}
	}
</script>


<style>
@import "../../common/css/font.css";
.clearfix{
	display: inline-block;
}
.clearfix:after{
	display: block;
	content: ".";
	height: 0;
	line-height: 0;
	clear: both;
	visibility: hidden;
}
.topheader{
	color: #fff;
	position: relative;
	background: rgba(7,17,27,0.5);
	overflow: hidden;
}
.header .content-wrapper{
	padding: 24px 12px 18px 24px;
	font-size: 0;
	position: relative;
}
.header .background{
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	z-index: -1;
	filter: blur(10px);
}
.header .detail{
	position: fixed;
	z-index: 100;
	width: 100%;
	height: 100%;
	overflow: auto;
	background: rgba(7,17,27,0.8);
	top: 0;
	left: 0;
}
.detail-wrapper{
	min-height: 100%;
	width: 100%;
}
.detail-main{
	margin-top: 64px;
	padding-bottom: 64px;
}
.detail-main .name{
	line-height: 16px;
	text-align: center;
	font-size: 16px;
	font-weight: 700;
}
.detail-close{
	position: relative;
	width: 32px;
	height: 32px;
	margin: -64px auto 0 auto;
	clear: both;
	font-size: 32px;
}
.header .bulletin-wrapper{
	height: 28px;
	line-height: 28px;
	padding: 0 22px 0 12px;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
	position: relative;
	background: rgba(7,17,27,0.2);
}
.header .bulletin-wrapper .icon-keyboard_arrow_right{
	position: absolute;
	font-size: 10px;
	right: 12px;
	top: 8px;
}
.bulletin-title{
	display: inline-block;
	vertical-align: top;
	margin-top: 8px;
	width: 22px;
	height: 12px;
	background-size: 22px 12px;
	background-repeat: no-repeat;
}
.bulletin-text{
	margin: 0 4px;
	font-size: 10px;
	vertical-align: top;
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.bulletin-title{
		background-image: url('./bulletin@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.bulletin-title{
		background-image: url('./bulletin@3x.png');
	}
}
.header .content-wrapper .avatar{
	display: inline-block;
	vertical-align: top;
}
.header .content-wrapper .avatar img{
	border-radius: 2px;
}
.header .content-wrapper .content{
	display: inline-block;
	margin-left: 16px;
}
.header .content-wrapper .support-count{
	position: absolute;
	right: 12px;
	bottom: 14px;
	padding: 0 8px;
	height: 24px;
	line-height: 24px;
	border-radius: 14px;
	background-color: rgba(0,0,0,0.2);
	text-align: center;
	vertical-align: top;
}
.header .content-wrapper .count{
	font-size: 10px;
}
.header .content-wrapper .icon-keyboard_arrow_right{
	font-size: 10px;
	line-height: 24px;
	margin-left: 2px;
}
.header .content-wrapper .content .title{
	margin: 2px 0 8px 0;
}
.header .content-wrapper .content .description{
	margin-bottom: 10px;
	line-height: 12px;
	font-size: 12px;
}
.header .content-wrapper .content .support{

}
.header .content-wrapper .content .support .icon{
	display: inline-block;
	width: 12px;
	height: 12px;
	margin-right: 4px;
	background-size: 12px 12px;
	background-repeat: no-repeat;
	vertical-align: top;
}
.header .content-wrapper .content .support .text{
	font-size: 10px;
	line-height: 12px;
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.header .content-wrapper .content .support .decrease{
		background-image: url('./decrease_1@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .support .decrease{
		background-image: url('./decrease_1@3x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.header .content-wrapper .content .support .discount{
		background-image: url('./discount_1@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .support .discount{
		background-image: url('./discount_1@3x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.header .content-wrapper .content .support .guarantee{
		background-image: url('./guarantee_1@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .support .guarantee{
		background-image: url('./guarantee_1@3x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.header .content-wrapper .content .support .invoice{
		background-image: url('./invoice_1@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .support .invoice{
		background-image: url('./invoice_1@3x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 2),(min-device-pixel-ratio: 2){
	.header .content-wrapper .content .support .special{
		background-image: url('./special_1@2x.png');
	}
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .support .special{
		background-image: url('./special_1@3x.png');
	}
}
.header .content-wrapper .content .title .brand{
	display: inline-block;
	width: 30px;
	height: 18px;
}
@media (-webkit-min-device-pixel-ratio: 3),(min-device-pixel-ratio: 3){
	.header .content-wrapper .content .title .brand{
		display: inline-block;
		width: 30px;
		height: 18px;
		background-image: url('./brand@3x.png');
		background-size: 30px 18px;
		background-repeat: no-repeat;
	}
}
.header .content-wrapper .content .title .brand{
	display: inline-block;
	vertical-align: top;
	width: 30px;
	height: 18px;
	background-image: url('./brand@2x.png');
	background-size: 30px 18px;
	background-repeat: no-repeat;
}
.header .content-wrapper .content .title .name{
	margin-left: 6px;
	font-size: 16px;
	line-height: 18px;
	font-weight: bold;
}


</style>

