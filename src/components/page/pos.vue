<template>
	<div class="pos">
		<leftNav></leftNav>
		<div class="main">
			<el-row>
				<el-col :span='10' class='fullHeight order'>
					<el-tabs>
						<el-tab-pane label="点餐">
							<el-table :data='orderList' border style="width:100%;text-align:center;" show-summary stripe>
							<el-table-column prop='name' label='商品' header-align="center"></el-table-column>
							<el-table-column prop='price' label='单价' header-align="center"></el-table-column>
							<el-table-column prop='count' label='数量' header-align="center"></el-table-column>
							<el-table-column prop='total' label='总价' header-align="center"></el-table-column>
							<el-table-column prop='operator' label='操作' header-align="center">
								<template slot-scope="scope">
									<el-button type="primary" icon="el-icon-circle-plus" circle @click="addOrder(scope.row)"></el-button>
									<el-button type="danger" icon="el-icon-delete" circle></el-button>
								</template>
							</el-table-column>
						</el-table>
						<br><br>
						<el-button type="warning" >挂单</el-button>
						<el-button type="danger" >删除</el-button>
						<el-button type="success" >结账</el-button>
						</el-tab-pane>
						<el-tab-pane label="挂单"></el-tab-pane>
						<el-tab-pane label="外卖"></el-tab-pane>
					</el-tabs>
				</el-col>
				<el-col :span='14' class='fullHeight space-left'>
					<div class="selling">
						<div class="title">畅销商品</div>
						<div class="sellingList">
							<ul>
								<li v-for="goods in sellingGoodsList"><el-button type="primary" plain>{{goods.name}} {{goods.price}}</el-button></li>
							</ul>
						</div>
						<div class="cb"></div>
					</div>
					<el-tabs>
						<el-tab-pane label="推荐">
							<div class="intro">
								<ul class="intro-food">
									<li v-for="item in introList">
										<div class="intro-card">
											<img :src="item.img">
											<div class="intro-name">{{item.name}}</div>
											<div class="intro-price">{{item.price}}</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="汉堡">
							<div class="hb">
								<ul class="hb-food">
									<li v-for="item in hb">
										<div class="hb-card">
											<img :src="item.goodsImg">
											<div class="hb-name">{{item.goodsName}}</div>
											<div class="hb-price">￥{{item.price}}元</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="小食">
							<div class="xs">
								<ul class="xs-food">
									<li v-for="item in xs">
										<div class="xs-card">
											<img :src="item.goodsImg">
											<div class="xs-name">{{item.goodsName}}</div>
											<div class="xs-price">￥{{item.price}}元</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="饮料">
							<div class="yl">
								<ul class="yl-food">
									<li v-for="item in yl">
										<div class="yl-card">
											<img :src="item.goodsImg">
											<div class="yl-name">{{item.goodsName}}</div>
											<div class="yl-price">￥{{item.price}}元</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="套餐">
							<div class="tc">
								<ul class="tc-food">
									<li v-for="item in tc">
										<div class="tc-card">
											<img :src="item.goodsImg">
											<div class="tc-name">{{item.goodsName}}</div>
											<div class="tc-price">￥{{item.price}}元</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
					</el-tabs>
				</el-col>
			</el-row>
		</div>
	</div>
</template>

<script type="text/javascript">
	import leftNav from '@/components/nav/leftNav'
	import axios from 'axios'
	export default{
		name:'pos',
		data(){
			return{
				orderList:[
					{
						id:1,
						name:'可乐',
						price:3,
						count:2,
						total:6
					},
					{
						id:2,
						name:'汉堡',
						price:10,
						count:1,
						total:10
					},
					{
						id:3,
						name:'鸡翅',
						price:10,
						count:2,
						total:20
					}
				],
				sellingGoodsList:[
					{
						id:1,
						name:"可乐",
						price:"￥3元"
					},
					{
						id:2,
						name:"汉堡",
						price:"￥10元"
					},
					{
						id:3,
						name:"鸡翅",
						price:"￥10元"
					},
					{
						id:4,
						name:"鸡米花",
						price:"￥6元"
					},
					{
						id:5,
						name:"奶茶",
						price:"￥5元"
					},
					{
						id:6,
						name:"上校鸡块",
						price:"￥15元"
					},
					{
						id:7,
						name:"鸡肉卷",
						price:"￥20元"
					}
				],
				introList:[
					{
						id:1,
						name:"可乐",
						price:"￥3元",
						img:'../static/food/kele.jpg'
					},
					{
						id:2,
						name:"汉堡",
						price:"￥10元",
						img:'../static/food/hanbao.jpg'
					},
					{
						id:3,
						name:"鸡翅",
						price:"￥10元",
						img:'../static/food/jichi.jpg'
					},
					{
						id:4,
						name:"鸡米花",
						price:"￥6元",
						img:'../static/food/jimihua.jpg'
					},
					{
						id:5,
						name:"奶茶",
						price:"￥5元",
						img:'../static/food/naicha.jpg'
					},
					{
						id:6,
						name:"上校鸡块",
						price:"￥15元",
						img:'../static/food/sxjk.jpg'
					},
					{
						id:7,
						name:"鸡肉卷",
						price:"￥20元",
						img:'../static/food/jrj.jpg'
					}
				],
				hb:[],
				xs:[],
				yl:[],
				tc:[]
			}
		},
		components:{
			leftNav
		},
		mounted:function(){
			var height = $(window).height();
			$(".fullHeight").height(height);
		},
		created(){
			axios.get('http://jspang.com/DemoApi/typeGoods.php').then(response => {
				this.hb = response.data[0];
				this.xs = response.data[1];
				this.yl = response.data[2];
				this.tc = response.data[3];
			}).catch(error => {
				console.log(error);
			});
		},
		methods:{
			addOrder(goods){
				goods.count ++ ;
			}
		},
		watch:{
			orderList:{								//监听对象属性变化
				handler:function(obj){
					for(let i in obj)
					{
						obj[i].total = obj[i].count * obj[i].price;
					}
				},
				deep:true							//必须加入这一句
			}
		}
	}
</script>

<style scoped>
	.main{
		width: 94%;
		float: right;
	}
	@media screen and (max-width: 1000px) {
	    .main{
			width: 89%;
		}
	}
	.sellingList ul{

	}
	ul li{
		list-style-type: none;
	}
	.sellingList ul li{
		float: left;
		margin: 20px 20px;
		font-size: 12px;
		cursor: pointer;
		font-weight: 600;
	}
	.title{
		text-align: left;
		padding: 10px 0 10px 10px;
		border-bottom: 1px solid #ccc;
	}
	.order{
		border-right: 2px solid #ccc;
	}
	.cb{
		clear: both;
	}
	.selling{
		border-bottom: 2px solid #ccc;
	}
	.space-left{
		padding-left: 20px;
	}
	ul.intro-food li,ul.hb-food li,ul.xs-food li,ul.yl-food li,ul.tc-food li{
		float: left;
		width: 21%;
		padding: 20px 10px;
		background-color: #f7f4f4;
		margin: 20px 1%;
	}
	ul.intro-food li img,ul.hb-food li img,ul.xs-food li img,ul.yl-food li img,ul.tc-food li img{
		width: 40%;
		float: left;
		height: 50px;
	}
	.intro-name,.hb-name,.xs-name,.yl-name,.tc-name{
		margin-bottom: 10px;
		color:red;
		text-align: right;
		margin-right: 20px;
	}
	.intro-price,.hb-price,.xs-price,.yl-price,.tc-price{
		text-align: right;
		margin-right: 20px;
	}
</style>