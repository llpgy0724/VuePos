<template>
  <div class="right">
    <div class="header">
      常用商品
    </div>
    <div class="main">
      <ul class="clearfix">
        <li v-for="food in oftenfoods">
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
            <li v-for="food in typefoods[0]">
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
            <li v-for="food in typefoods[1]">
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
            <li v-for="food in typefoods[2]">
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
            <li v-for="food in typefoods[3]">
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
</template>

<script>
import axios from 'axios'

export default {
  name: 'right',
  created: function () {
    //热门食物
    axios.get('http://jspang.com/DemoApi/oftenGoods.php')
    .then(reponse => {
      //consconsole.log(reponse)
      this.oftenfoods = reponse.data;
    })
    .catch(error => {
      alert("信息获取失败!")
    })

    //right bottom
    axios.get('http://jspang.com/DemoApi/typeGoods.php')
    .then(reponse => {
      this.typefoods[0] = reponse.data[0];
      this.typefoods[1] = reponse.data[1];
      this.typefoods[2] = reponse.data[2];
      this.typefoods[3] = reponse.data[3];
    })
    .catch(error => {
      alert("获取数据失败")
    })
  },
  data() {
    return {
      oftenfoods: [],
      typefoods: [
        {},
        {},
        {},
        {}
      ]
    }
  },
  methods: {
    addOrderList 
  }
}
</script>

<style lang="scss">
  .clearfix{overflow:auto;_height:1%}
  .right{
    float: left;
    width: 60%;
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
</style>
