<template>
  <div class="end-main">
    <div class="middle">
      <div class="header">
        <el-tabs activeName="first">
          <el-tab-pane label="点餐" name="first">
            <el-table :data="dataMiddle" border stripe style="width:100%">
              <el-table-column prop="goodsName" label="商品名称"></el-table-column>
              <el-table-column prop="count" label="数量"></el-table-column>
              <el-table-column prop="price" label="金额">
                <template scope="scope">
                  {{ scope.row.count*scope.row.price }}
                </template>
              </el-table-column>
              <el-table-column flxed label="操作">
                <template scope="scope">
                  <el-button @click.native.prevent="deleteOne(scope.row)" type="text" size="small">移除</el-button>
                  <el-button @click.native.prevent="addOrderList(scope.row)" type="text" size="small">增加</el-button>
                </template>
              </el-table-column>
            </el-table>
            <div class="end" v-show="endcount">
              <div class="end_count">
                <small>数量:</small>
                <span>{{ endcount }}</span>
              </div>
              <div class="end_price">
                <small>金额:</small>
                <span>{{ endmoney }}元</span>
              </div>
            </div>
            <div class="middle_bottom_button">
              <el-button type="warning">挂单</el-button>
              <el-button type="danger" @click="delAll">删除</el-button>
              <el-button type="success" @click="checkOut">结账</el-button>
            </div>
          </el-tab-pane>
          <el-tab-pane label="挂单" name="second">挂单</el-tab-pane>
          <el-tab-pane label="外卖" name="third">外卖</el-tab-pane>
        </el-tabs>
      </div>  
    </div>
    <div class="right">
      <div class="header">
        常用商品
      </div>
      <div class="main">
        <ul class="clearfix">
          <li v-for="food in oftenfoods" @click="addOrderList(food)">
            <el-button>
              <span>{{food.goodsName}}</span>
              <span class="o-price">￥{{food.price}}</span>
            </el-button>
          </li>
          
        </ul>
      </div>
      <div class="bottom">
        <el-tabs activeName="hanbao">
          <el-tab-pane label="汉堡" name="hanbao">
            <ul class="clearfix">
              <li v-for="food in typefood[0]" @click="addOrderList(food)">
                <span>
                  <img :src="food.goodsImg" alt="">
                </span>
                <span>
                  {{ food.goodsName }}
                </span>
                <span>
                  ￥{{ food.price }}元
                </span>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="小食" name="xiaoshi">
            <ul class="clearfix">
              <li v-for="food in typefood[1]" @click="addOrderList(food)">
                <span>
                  <img :src="food.goodsImg" alt="">
                </span>
                <span>
                  {{ food.goodsName }}
                </span>
                <span>
                  ￥{{ food.price }}元
                </span>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="饮料" name="yinliao">
            <ul class="clearfix">
              <li v-for="food in typefood[2]" @click="addOrderList(food)">
                <span>
                  <img :src="food.goodsImg" alt="">
                </span>
                <span>
                  {{ food.goodsName }}
                </span> 
                <span>
                  ￥{{ food.price }}元
                </span>
              </li>
            </ul>
          </el-tab-pane>
          <el-tab-pane label="套餐" name="taocan">
            <ul class="clearfix">
              <li v-for="food in typefood[3]" @click="addOrderList(food)">
                <span>
                  <img :src="food.goodsImg" alt="">
                </span>
                <span>
                  {{ food.goodsName }}
                </span>
                <span>
                  ￥{{ food.price }}元
                </span>
              </li>
            </ul>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
    <div class="clearfix"></div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  name: 'end-main',
  data() {
    return {
      endcount: 0,
      endmoney: 0,
      endshow: 0,
      dataMiddle: [],
      oftenfoods: [],
      typefood: [{},{},{},{}]
      // typefood0: [],
      // typefood1: [],
      // typefood2: [],
      // typefood3: []
    }
  },
  created: function () {
    //热门食物
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    .then(reponse => {
      //consconsole.log(reponse)
      this.oftenfoods = reponse.data;
    })
    .catch(error => {
      alert("信息获取失败!")
    });

    //right bottom
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(reponse => {

      this.typefood[0] = reponse.data[0];
      this.typefood[1] = reponse.data[1];
      this.typefood[2] = reponse.data[2];
      this.typefood[3] = reponse.data[3];
      
    })
    .catch(error => {
      alert("获取数据失败");
    });
  },
  methods: {
    totoal: function () {
      this.endcount = 0;//总计数量
      this.endmoney = 0;//总额
      this.dataMiddle.forEach((element) => {
        this.endcount += element.count;
        this.endmoney = this.endmoney + (element.price * element.count);
      })
    },
    isHave: function(datas) {
      var arr = this.dataMiddle.filter(item => item.goodsId == datas.goodsId);
      return arr;
    },
    addOrderList: function(datas) {
      var arr = this.isHave(datas);
      if (arr.length) {
        arr[0].count++
      }else{
        var newFood = { goodsId: datas.goodsId, goodsName: datas.goodsName, price: datas.price, count: 1 }
        this.dataMiddle.push(newFood)
      }
      this.totoal()
    },
    deleteOne(datas) {
      this.dataMiddle = this.dataMiddle.filter(item => item.goodsId!=datas.goodsId)
      this.totoal();
    },
    delAll() {
      this.dataMiddle = []
      this.totoal();
    },
    checkOut() {
      if(this.endcount){
        this.$message({
          message: '结账成功，继续努力~！',
          type: 'success'
        })
        this.delAll()
      }else{
        this.$message({
          message: '请选择需要结账的食品哦~！',
          type: 'warning'
        })
      }
    }
  }
}
</script> 

<style lang="scss">
  .end-main{
    float: left;
    height: 100%;
    width: 95%;
    .middle {
      float: left;
      width: 30%;
      height: 100%;
      border-right: 1px solid #c0ccda;
      box-sizing: border-box;
      overflow: auto;
      .el-table .cell {
        padding: 0;
        text-align: center;
      }
      .end {
        height: 41px;
        line-height: 41px;
        border-bottom: 1px solid #D3DCE6;
        div{
          display: inline;
          small {
            margin-left: 15px;
          }
        }
        .end_count{
          span{
            color: #6e8299;
          }
        }
        .end_price{
          span{
            color: #FF5722;
          }
        }
      }
      .middle_bottom_button{
        margin-top: 15px;
      }
    }
    .clearfix{overflow:auto;_height:1%}
    .right{
      float: left;
      width: 70%;
      height: 100%;
      .header{
        height: 41px;
        line-height: 41px;
        border-bottom: 1px solid #c0ccda;
      }
      .main{
        ul{
          list-style-type: none;
          li{
            float: left;
            margin: 6px;
            span{
              font-size: 16px;
            }
            .o-price{
              color: #58b7ff;
            }
          }
        }
      }
      .bottom{
        ul{
          li{
            float: left;
            width: 23%;
            margin: 2px;
            border: 1px solid #e5e9f2;
            height: auto;
            overflow: hidden;
            background-color: #fff;
            padding: 2px;
            cursor: pointer;
            span{
              display: block;
              float: left;
            }
            span:nth-child(1){
              width: 40%;
              img{
                width: 100%;
              }
            }
            span:nth-child(2){
              font-size: 16px;
              padding-left: 10px;
              color: brown;
            }
            span:nth-child(3){
              font-size: 16px;
              padding-left: 10px;
              padding-top: 10px;
            }
          }
        }
      }
    }
  }
</style>
