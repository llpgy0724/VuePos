<template>
  <div class="left-nav">
    <ul>
      <li>
        <i class="mybig myicon my-icon-jiezhang"></i>
        <span>收银</span>
      </li>
      <li>
        <i class="mybig myicon my-icon-dianpu"></i>
        <span>店铺</span>
      </li>
      <li>
        <i class="mybig myicon my-icon-iconfontshangpin"></i>
        <span>商铺</span>
      </li>
      <li>
        <i class="mybig myicon my-icon-huiyuan"></i>
        <span>会员</span>
      </li>
      <li>
        <i class="mybig myicon my-icon-tongji"></i>
        <span>统计</span>
      </li>
      <li>
        <i class="mybig myicon my-icon-shezhi"></i>
        <span>设置</span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  methods: {
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
  @import url('../assets/css/iconfont.css');
  .left-nav{
    float: left;
    width: 5%;
    height: 100%;
    background-color: #1DBCE0;
    color: #fff;
    box-sizing: border-box;
    ul{
      list-style-type: none;
      margin:0;
      padding: 0;
      li{
        padding: 10px;
        border-bottom:1px solid #20a0ff;
        &:hover{
          cursor: pointer;
        }
        .mybig{
          font-size: 22px;
        }
        span{
          font-size: 12px;
          display: block;
        }
      }
    }
  }
</style>

