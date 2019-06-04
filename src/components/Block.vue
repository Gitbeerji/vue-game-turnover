<template>
  <div v-bind:class="[cardClass, openClass, matchClass]" v-on:click="openBlock">
    <div class="card-wrap">
        <div class="card">
          <i v-bind:class="[iconClass, signClass]"></i>
        </div>
      </div>
  </div>
</template>

<script>
/* eslint-disable */
export default {
  name: 'Block',
  props: [
    'block',
    'match',
    'step',
    'index',
    'isInit',
    'itemCount'
  ],
  data () {
    return {
      iconClass: 'icon',
      openClass: '',
      matchClass: '',
    }
  },
  computed: {
    signClass (){
      return this.block.content
    },
    cardClass (){
      return 'card-item card-item-' + this.itemCount
    }
  },
  watch: {
    isInit (val, oldVal){
      if( val && val == 'init' ){
        this.init()
      }
    }
  },
  methods: {
    init (){
      this.openClass = ''
      this.matchClass = ''
    },
    openBlock (){
      let step = this.step
      if( this.openClass == "open show" || this.matchClass == "open match" ){
        return
      }
      if( !this.match ){
        return
      }
      this.$emit('addStep')
      step ++
      this.openClass="open show"
      if( parseInt(step) % 2 == 0 ){
        this.$emit('matchBlock', {index: this.index, content: this.block.content})
        return
      }
      this.sendFirstBlock()
    },
    closeBlock (){
      this.openClass = ""
    },
    matchBlock (){
      this.openClass = ""
      this.matchClass = "open match"
    },
    sendFirstBlock (){
      let data = {index: this.index, content: this.block.content}
      //console.log(data)
      this.$emit('getFirstBlock', data);
    }
  }
}
</script>

<style scoped>
.card-item {
  position: relative;
  width: 25%;
  padding-top: 25%;
}
.card-item-2 {
  width: 50%;
  padding-top: 50%;
}
.card-item-4 {
  width: 25%;
  padding-top: 25%;
}
.card-item-6 {
  width: 16.66%;
  padding-top: 16.66%;
}
.card-wrap {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  padding: 4px;
}
.card {
  width: 100%;
  height: 100%;
  background: rgba(98,152,111,.2);
  font-size: 0;
  color: #ffffff;
  border-radius: 8px;
  overflow: hidden;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 5px 2px 20px 0 rgba(46, 61, 73, 0.5);
  transform: rotateY(180deg);
  transition: transform 0.3s;
}

.deck .match .card {
    cursor: default;
    background: #02ccba;
    font-size: 33px;
    animation: fbig 0.3s alternate;
}
@keyframes fbig {
    from{transform: scale(1)}
    to {transform: scale(1.1)}
}

.card .icon.a {
	background-image: url(../assets/a.jpg);
}
.card .icon.b {
	background-image: url(../assets/b.jpg);
}
.card .icon.c {
	background-image: url(../assets/c.jpg);
}
.card .icon.d {
	background-image: url(../assets/d.jpg);
}
.card .icon.e {
	background-image: url(../assets/e.jpg);
}
.card .icon.f {
	background-image: url(../assets/f.jpg);
}
.card .icon.g {
	background-image: url(../assets/g.jpg);
}
.card .icon.h {
	background-image: url(../assets/h.jpg);
}
.card .icon.i {
	background-image: url(../assets/i.jpg);
}
.card .icon.j {
	background-image: url(../assets/j.jpg);
}
.card .icon.k {
	background-image: url(../assets/k.jpg);
}
.card .icon.l {
	background-image: url(../assets/l.jpg);
}
.card .icon.m {
	background-image: url(../assets/m.jpg);
}
.card .icon.n {
	background-image: url(../assets/n.jpg);
}
.card .icon.o {
	background-image: url(../assets/o.jpg);
}
.card .icon.p {
	background-image: url(../assets/p.jpg);
}
.card .icon.q {
	background-image: url(../assets/q.jpg);
}
.card .icon.r {
	background-image: url(../assets/r.jpg);
}


</style>
