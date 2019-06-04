<template>
  <div>
    <div class="header">
      <h1>薇妮翻牌游戏</h1>
      <div class="tips clear">
        <div class="left">
          V币: <span>0</span>
        </div>
        <div class="right">
          可玩次数: <span>3</span>
        </div>
      </div>
    </div>
    <div class="button-wrap">
      <div class="">
        <a v-on:click="toMain" type="button" name="button">开始游戏</a>
      </div>
      <div class="">
        <a type="button" name="button">游戏说明</a>
      </div>
      <div class="">
        <a type="button" name="button">排行榜</a>
      </div>
      <div class="">
        <a type="button" name="button">分享赢V币</a>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Index',
  data () {
    return {

    }
  },
  methods: {
    toMain: function () {
      this.$router.push({path: 'Main'})
    }
  }
}
</script>
<style scoped>
  .clear:after,
  .clear:before {
    content: '';
    display: block;
    clear: both;
  }
  .header h1 {
    padding: 30px 0;
    text-align: center;
    margin-bottom: 30px;
  }
  .tips {
    padding: 0 5%;
    margin-bottom: 30px;
  }
  .tips .left {
    float: left;
  }
  .tips .right {
    float: right;
  }
  .button-wrap {
    text-align: center;
  }
  .button-wrap > div {
    margin-bottom: 20px;
  }
  .button-wrap a {
    display: inline-block;
    border: 0;
    background: #2EAF7A;
    color: #FFF;
    width: 40%;
    font-size: 20px;
    padding: 5px 0;
    border-radius: 5px;
    outline: 0;
  }
</style>
