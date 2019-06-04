<template>
  <header>
    <div class="top clear">
      <div class="left">
        <span>第{{level}}关</span>
      </div>
      <div class="right">
        当前得分: <span>{{point}}</span>
      </div>
    </div>
    <div class="tips clear">
      <div class="left">
        步数: <span>{{step}}</span>
      </div>
      <div class="right">
        TIME: <span>{{time}}</span>
      </div>
    </div>
  </header>
</template>
<script>
export default {
  props: [
    'level',
    'point',
    'step',
    'time'
  ]
}
</script>
<style scoped>
header {
  padding: 2% 5%;
}
.clear:before,
.clear:after {
  content: '';
  display: block;
  clear: both;
}
.top {
  font-size: 22px;
}
.left {
  float: left;
}
.right {
  float: right;
}
</style>
