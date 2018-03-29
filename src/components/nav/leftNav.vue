<template>
	<div class="leftNav">
		<ul class="navList">
			<li>
				<div class="item">
					<i class="iconfont">&#xe674;</i><br>
					<span>收银</span>
				</div>
			</li>
			<li>
				<div class="item">
					<i class="iconfont">&#xe66d;</i><br>
					<span>店铺</span>
				</div>
			</li>
			<li>
				<div class="item">
					<i class="iconfont">&#xe679;</i><br>
					<span>商品</span>
				</div>
			</li>
			<li>
				<div class="item">
					<i class="iconfont">&#xe678;</i><br>
					<span>会员</span>
				</div>
			</li>
			<li>
				<div class="item">
					<i class="iconfont">&#xe677;</i><br>
					<span>统计</span>
				</div>
			</li>
		</ul>
	</div>
</template>

<script type="text/javascript">
	export default{
		name:'leftNav',
		mounted:function(){
			var height = $(window).height();
			$(".leftNav").height(height);
		}
	}	
</script>


<style scoped>
	.leftNav{
		float: left;
		font-size: 20px;
		width: 5%;
		background-color: #0186E0;
	}
	@media screen and (max-width: 1000px) {
	    .leftNav{
			width: 10%;
		}
	}
	.navList i{
		font-size: 25px;
	}
	ul.navList li{
		display: block;
		text-align: center;
		color: white;
		padding: 20px 1px;
		margin: 10px 0;
		cursor: pointer;
	}
	ul.navList li:hover{
		background-color: #0056c1;
    	color: #ffda22;
	}
	.item{
		width: 100%;
	}
</style>