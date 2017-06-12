<template>
    <div class="pos">
        <div>
            <el-row >
                <el-col :span="8" id="order-list" style="background: #eee">
                    <el-tabs type="card">
                        <el-tab-pane label="点餐">
                            <el-table :data='tableData' stripe>
                                <el-table-column label="商品名称" prop="goodsName" ></el-table-column>
                                <el-table-column label="数量" prop="count" width="70"></el-table-column>
                                <el-table-column label="单价" prop="price" width="70"></el-table-column>
                                <el-table-column label="操作" fixed="right">
                                    <template scope="scope">
                                        <el-button type="text" icon="plus" size="mini" @click="addOrderList(scope.row)"></el-button>
                                        <el-button type="text" icon="delete" size="mini" @click="delSingleGood(scope.row)"></el-button>
                                    </template>
                                </el-table-column>
                            </el-table>
                            <div class="total">
                                <div class="count">数量: <span>{{totalCount}}</span></div>
                                <div class="money">总金额: <span>{{totalMoney}}</span>元</div>
                            </div>
                            <div class="controls" style="margin-top:20px">
                                <el-button  type="warning">挂单</el-button>
                                <el-button  type="danger" @click="deleteAllGoods()">删除</el-button>
                                <el-button  type="success" @click="checkout()">结账</el-button>
                            </div>
                        </el-tab-pane>
                        <!--<el-tab-pane label="外卖">-->
                            <!--<el-table :data='tableData' stripe>-->
                                <!--<el-table-column label="商品名称" prop="goodsName" ></el-table-column>-->
                                <!--<el-table-column label="数量" prop="count" width="70"></el-table-column>-->
                                <!--<el-table-column label="单价" prop="price" width="70"></el-table-column>-->
                                <!--<el-table-column label="操作" fixed="right">-->
                                    <!--<template scope="scope">-->
                                        <!--<el-button type="text" icon="plus" size="mini" @click="addOrderList(scope.row)"></el-button>-->
                                        <!--<el-button type="text" icon="delete" size="mini" @click="delSingleGood(scope.row)"></el-button>-->
                                    <!--</template>-->
                                <!--</el-table-column>-->
                            <!--</el-table>-->
                            <!--<div class="total">-->
                                <!--<div class="count">数量: <span>{{totalCount}}</span></div>-->
                                <!--<div class="money">总金额: <span>{{totalMoney}}</span>元</div>-->
                            <!--</div>-->
                            <!--<div class="controls" style="margin-top:20px">-->
                                <!--<el-button  type="warning">挂单</el-button>-->
                                <!--<el-button  type="danger" @click="deleteAllGoods()">删除</el-button>-->
                                <!--<el-button  type="success" @click="checkout()">结账</el-button>-->
                            <!--</div>-->
                        <!--</el-tab-pane>-->
                        <el-tab-pane label="我">
                            <img src="./../../../static/img/avatar.png" >
                            <p style="padding:30px 10px 10px 10px">Lily</p>
                            <p style="height: 18px;line-height: 18px;padding:40px 30px"><a target="_blank" href="http://github.com/sunyuqing">GitHub: http://github.com/sunyuqing</a></p>
                            <p style="height: 18px;line-height: 18px;"><a target="_blank" href="http://yuqingsun.com">我的博客: http://yuqingsun.com</a></p>
                            <p style="height: 18px;line-height: 18px;padding:40px 30px""><a  href="javascript:;">我的邮箱: sunnyday0824@163.com </a></p>
                        </el-tab-pane>
                    </el-tabs>
                </el-col>
                <el-col :span="16" >
                    <div class="popular-goods">
                        <div class="title">热销榜 <i class="icon iconfont icon-31rexiao" style='color: red'></i></div>
                        <div class="pop-goods-list">
                            <ul  >
                                <li style="cursor: pointer" v-for="item in oftenGoods" @click="addOrderList(item)">
                                    <span>{{item.goodsName}}
                                    </span><span class="item-price">￥{{item.price}}元</span>
                                </li>
                            </ul>
                        </div>
                    </div>
                    <div class="goods-type" style="clear: both">
                        <el-tabs>
                            <el-tab-pane label="汉堡主食">
                                <ul class='cookList'>
                                    <li v-for="goods in type0Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="40" height="40"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="美味小吃">
                                <ul class='cookList'>
                                    <li v-for="goods in type1Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="40" height="40"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="饮品">
                                <ul class='cookList'>
                                    <li v-for="goods in type2Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="40" height="40"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label="超值套餐" >
                                <ul class='cookList'>
                                    <li v-for="goods in type3Goods" @click="addOrderList(goods)">
                                        <span class="foodImg"><img :src="goods.goodsImg" width="40" height="40"></span>
                                        <span class="foodName">{{goods.goodsName}}</span>
                                        <span class="foodPrice">￥{{goods.price}}元</span>
                                    </li>
                                </ul>
                            </el-tab-pane>

                        </el-tabs>
                    </div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>

<script type="text/ecmascript-6">
    import axios from 'axios';
    export default {
        data() {
            return {
                tableData: [],
                oftenGoods: [],
                type0Goods: [],
                type1Goods: [],
                type2Goods: [],
                type3Goods: [],
                totalMoney: 0,
                totalCount: 0
            };
        },
        created() {
            axios.get('http://jspang.com/DemoApi/oftenGoods.php')
                    .then(res => {
                        this.oftenGoods = res.data;
                    })
                    .catch(error => {
                        console.log(error);
                        alert('网络错误，不能访问');
                    });
            axios.get('http://jspang.com/DemoApi/typeGoods.php')
                    .then(res => {
                        console.log(res);
                        this.type0Goods = res.data[0];
                        this.type1Goods = res.data[1];
                        this.type2Goods = res.data[2];
                        this.type3Goods = res.data[3];
                    })
                    .catch(error => {
                        console.log(error);
                        alert('网络错误，不能访问');
                    });
        },
        mounted() {
            const orderHeight = document.body.clientHeight;
            document.getElementById('order-list').style.height = orderHeight + 'px';
        },
        methods: {
            addOrderList(goods) {
                this.totalMoney = 0;
                this.totalCount = 0;

                // 商品是否已经存在于订单列表中
                let isHave = false;
                for (let i = 0; i < this.tableData.length; i++) {
                    if (this.tableData[i].goodsId === goods.goodsId) {
                        isHave = true;
                    }
                }
                // 根据判断的值编写业务逻辑
                if (isHave) {
                    // 改变列表中的数量
                    let arr = this.tableData.filter(item => item.goodsId === goods.goodsId);
                    arr[0].count++;
                } else {
                    let newGoods = {
                        goodsId: goods.goodsId,
                        goodsName: goods.goodsName,
                        price: goods.price,
                        count: 1
                    };
                    this.tableData.push(newGoods);
                }
                this.$message({
                    message: '商品添加成功。',
                    type: 'success'
                });
                //  计算汇总金额和数量
                this.getTotal();
            },
            //  删除单个商品
            delSingleGood(good) {
                this.tableData = this.tableData.filter(item => item.goodsId !== good.goodsId);
                this.getTotal();
                this.$message({
                    message: '商品删除成功。',
                    type: 'success'
                });
            },
            // 删除所有商品
            deleteAllGoods() {
                if (this.totalCount === 0) {
                    this.$message({
                        message: '您还没有选择任何商品',
                        type: 'info'
                    });
                } else {
                    this.$confirm('此操作将删除所有已选商品, 是否继续?', '提示', {
                        confirmButtonText: '确定',
                        cancelButtonText: '取消',
                        type: 'warning'
                    }).then(() => {
                        this.tableData = [];
                        this.totalCount = 0;
                        this.totalMoney = 0;
                        this.$message({
                            type: 'success',
                            message: '为您删除成功!'
                        });
                    }).catch(() => {
                        this.$message({
                            type: 'info',
                            message: '已取消删除。'
                        });
                    });
                }
            },
            //  汇总数量与金额
            getTotal() {
                this.totalCount = 0;
                this.totalMoney = 0;
                if (this.tableData) {
                    this.tableData.forEach((ele) => {
                        this.totalCount += ele.count;
                        this.totalMoney += this.totalMoney + (ele.price * ele.count);
                    });
                }
            },
            //  结账
            checkout() {
                if (this.totalCount !== 0) {
                    this.tableData = [];
                    this.totalCount = 0;
                    this.totalMoney = 0;
                    this.$message({
                        message: '结账成功，期待您下次光临。',
                        type: 'success'
                    });
                } else {
                    this.$message({
                        message: '欢迎光临，请先选择商品。',
                        type: 'info'
                    });
                }
            }
        }
    };
</script>

<style lang="stylus" rel="stylesheet/stylus" scoped>
.total
    background: #fff
    padding: 10px
    border-bottom: 1px solid #ccc
    font-size: 10px
    .count,.money
        display: inline-block
        margin:0 20px
        color: #1D8CE0
.popular-goods
    .title
        height: 21px
        border-bottom: 1px solid #D3DCE6
        padding: 10px
        background: #F9FAFC
        /*font-weight: 700*/
    .pop-goods-list
        li
            float: left
            border: 1px solid #E5E9F2
            padding: 10px
            margin: 5px
            background-color: #fff
            .item-price
                color: #58B7FF
.goods-type
    .cookList
        li
            list-style: none
            width: 23%
            border: 1px solid #E5E9F2
            height: auto
            overflow: hidden
            background-color:#fff
            padding: 8px 2px
            float:left
            margin: 2px
            cursor: pointer
            span
                display: block
                float: left
                &.foodImg
                    width: 40%
                &.foodName
                    font-size: 18px
                    padding-left: 10px
                    color: brown
                &.foodPrice
                    font-size: 16px
                    padding-left: 10px
                    padding-top: 10px
</style>
