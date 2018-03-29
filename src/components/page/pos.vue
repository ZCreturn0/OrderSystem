<template>
	<div class="pos">
		<leftNav></leftNav>
		<div class="main">
			<el-row>
				<el-col :span='10' class='fullHeight order'>
					<el-tabs>
						<el-tab-pane label="点餐">
							<el-table :data='orderList' border style="width:100%;text-align:center;" show-summary stripe>
							<el-table-column prop='goodsName' label='商品' header-align="center"></el-table-column>
							<el-table-column prop='price' label='单价' header-align="center"></el-table-column>
							<el-table-column prop='count' label='数量' header-align="center"></el-table-column>
							<el-table-column prop='total' label='总价' header-align="center"></el-table-column>
							<el-table-column prop='operator' label='操作' header-align="center">
								<template slot-scope="scope">
									<el-button type="primary" icon="el-icon-circle-plus" circle @click="addOrder(scope.row)"></el-button>
									<el-button type="danger" icon="el-icon-delete" circle @click="deleteSingle(scope.row)"></el-button>
								</template>
							</el-table-column>
						</el-table>
						<br><br>
						<el-button type="warning" >挂单</el-button>
						<el-button type="danger" @click="deleteOrder">删除</el-button>
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
								<li v-for="goods in sellingGoodsList"><el-button type="primary" plain>{{goods.goodsName}} ￥{{goods.price}}元</el-button></li>
							</ul>
						</div>
						<div class="cb"></div>
					</div>
					<el-tabs>
						<el-tab-pane label="推荐">
							<div class="intro">
								<ul class="intro-food">
									<li v-for="item in introList" @click="makeOrder(item)">
										<div class="intro-card">
											<img :src="item.goodsImg">
											<div class="intro-name">{{item.goodsName}}</div>
											<div class="intro-price">￥{{item.price}}元</div>
										</div>
									</li>
								</ul>
							</div>
						</el-tab-pane>
						<el-tab-pane label="汉堡">
							<div class="hb">
								<ul class="hb-food">
									<li v-for="item in hb" @click="makeOrder(item)">
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
									<li v-for="item in xs" @click="makeOrder(item)">
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
									<li v-for="item in yl" @click="makeOrder(item)">
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
									<li v-for="item in tc" @click="makeOrder(item)">
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
						goodsId:11,
						goodsName:'可乐',
						price:3,
						count:2,
						total:6
					},
					{
						goodsId:12,
						goodsName:'汉堡',
						price:10,
						count:1,
						total:10
					},
					{
						goodsId:13,
						goodsName:'鸡翅',
						price:10,
						count:2,
						total:20
					}
				],
				sellingGoodsList:[
					{
						goodsId:11,
						name:"可乐",
						price:3
					},
					{
						goodsId:12,
						name:"汉堡",
						price:10
					},
					{
						goodsId:13,
						name:"鸡翅",
						price:10
					},
					{
						goodsId:4,
						name:"鸡米花",
						price:6
					},
					{
						goodsId:5,
						name:"奶茶",
						price:5
					},
					{
						goodsId:6,
						name:"上校鸡块",
						price:15
					},
					{
						goodsId:7,
						name:"鸡肉卷",
						price:20
					}
				],
				introList:[
					{
						goodsId:11,
						goodsName:"可乐",
						price:3,
						goodsImg:'static/food/kele.jpg'
					},
					{
						goodsId:12,
						goodsName:"汉堡",
						price:10,
						goodsImg:'static/food/hanbao.jpg'
					},
					{
						goodsId:13,
						goodsName:"鸡翅",
						price:10,
						goodsImg:'static/food/jichi.jpg'
					},
					{
						goodsId:4,
						goodsName:"鸡米花",
						price:6,
						goodsImg:'static/food/jimihua.jpg'
					},
					{
						goodsId:5,
						goodsName:"奶茶",
						price:5,
						goodsImg:'static/food/naicha.jpg'
					},
					{
						goodsId:6,
						goodsName:"上校鸡块",
						price:15,
						goodsImg:'static/food/sxjk.jpg'
					},
					{
						goodsId:7,
						goodsName:"鸡肉卷",
						price:20,
						goodsImg:'static/food/jrj.jpg'
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
			},
			makeOrder(item){
				if(this.orderExsist(item))			//如果同类型订单存在则count直接+1
				{
					for(let i in this.orderList)
					{
						if(this.orderList[i].goodsId == item.goodsId)
						{
							this.orderList[i].count++;
						}
					}
				}
				else
				{
					let new_order = {
						goodsId:item.goodsId,
						goodsName:item.goodsName,
						price:item.price,
						count:1
					};
					this.orderList.push(new_order);
				}
			},
			orderExsist(newOrder){					//判断同类型订单是否存在
				for(let i in this.orderList)
				{
					if(this.orderList[i].goodsId == newOrder.goodsId)
					{
						return true;
					}
				}
				return false;
			},
			deleteSingle(goods){
				this.orderList = this.orderList.filter(o => o.goodsId != goods.goodsId);		//filter: o:数组中每个元素      满足条件返回,不满足过滤
			},
			deleteOrder(){
				this.orderList = [];
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