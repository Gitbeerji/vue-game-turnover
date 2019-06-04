<template>
  <div>
    <Header
      :level="level"
      :point="point"
      :step="step"
      :time="timeShow"></Header>
    <section class="deck" id="deck">
      <Block
        ref="block"
        v-for="(block, index) in blocks"
        :block="block"
        :match="match"
        :key="index"
        :index="index"
        :step="step"
        :isInit="isInit"
        :itemCount="itemCount"
        v-on:addStep="addStep"
        v-on:matchBlock="matchBlock"
        v-on:getFirstBlock="getFirstBlock">
      </Block>
    </section>
  </div>
</template>

<script>
/* eslint-disable */
import Swal from 'sweetAlert2'
import Block from './Block'
import Header from './Header'

const imgArr = [
  {content: 'a'},{content: 'b'},{content: 'c'},{content: 'd'},{content: 'e'},{content: 'f'},
  {content: 'g'},{content: 'h'},{content: 'i'},{content: 'j'},{content: 'k'},{content: 'l'},
  {content: 'm'},{content: 'n'},{content: 'o'},{content: 'p'},{content: 'q'},{content: 'r'},
]

export default {
  name: 'Main',
  data () {
    return {
      level: 1,
      allLevel: 5,
      time: 0,
      step: 0,
      point: 0,
      match: true,
      isInit: null,
      timer: null,
      pass: false,
      levelData: [null,
        {count: 2, time: 120, itemCount: 2},
        {count: 6, time: 180, itemCount: 4},
        {count: 8, time: 120, itemCount: 4},
        {count: 15, time: 180, itemCount: 6},
        {count: 18, time: 120, itemCount: 6},
      ],
      gameCount: 0,
      firstBlock: null,
      blocks: null,
      itemCount: 0
    }
  },
  computed: {
    timeShow () {
      let format = (time) => {
        if( time < 10 ){
          return '0' + time
        }
        return time
      }
      let mintue = 0, second = 0;


      if( this.time > 60 ){
        mintue = parseInt( this.time / 60)
        second = parseInt( this.time % 60)
      }else{
        second = this.time
      }

      return format(mintue) + ':' + format(second)
    }
  },
  components: {
    Block, Header
  },
  created (){
    this.init()
  },
  destroyed (){
    clearInterval(this.timer)
    Swal.close()
  },
  methods: {
    //洗牌函数
    shuffle (array){
      let currentIndex = array.length, temporaryValue, randomIndex;
      while (currentIndex !== 0) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }
      return array;
    },
    init (){
      this.pass = false
      this.setp = 0
      this.match = true
      this.gameCount = 0
      this.firstBlock = null
      this.itemCount = this.levelData[this.level].itemCount
      this.time = this.levelData[this.level].time;
      clearInterval(this.timer)
      let _arr = imgArr.slice(0, this.levelData[this.level].count)
      this.blocks = this.shuffle(_arr.concat(_arr))
      //this.blocks = _arr.concat(_arr)
      this.timer = setInterval(this.timePass, 1000)
    },
    timePass (){
      if( this.pass ){
        clearInterval(this.timer)
        return;
      }
      if( this.time <= 0 ){
        this.time = 0;
        //游戏结束
        clearInterval(this.timer)
        Swal.fire({
          html: '<div>Game Over!</div>',
          confirmButtonText: '确定',
          confirmButtonClass: 'alertComfirm'
        }).then((result) => {
          if (result.value){
            this.$router.push({path: 'Index'})
          }
        })
        return;
      }
      this.time --
    },
    addStep () {
      this.step = this.step + 1
    },
    matchBlock (res) {
      this.match = !this.match
      if( res.content == this.firstBlock.content ){
        //匹配成功
        //console.log('yes');
        setTimeout(() => {
          this.matchedBlock(res.index)
          this.matchedBlock(this.firstBlock.index)
          this.firstBlock = null
          this.match = !this.match
          this.gameCount ++
          this.isPass()
        }, 500)
      }else{
        //匹配失败
        setTimeout(() => {
          this.closeBlock(res.index)
          this.closeBlock(this.firstBlock.index)
          this.firstBlock = null
          this.match = !this.match
        }, 500)
      }
    },
    getFirstBlock (res){
      this.firstBlock = res;
    },
    closeBlock (index){
      this.$refs.block[index].closeBlock()
    },
    matchedBlock (index){
      this.$refs.block[index].matchBlock()
    },
    isPass (){
      if( this.isInit ){
        this.isInit = null
      }
      if( this.gameCount == this.blocks.length /2 ){
        this.pass = true
        if( this.level >= this.allLevel){
          alert('通关')
          return;
        }
        this.nextLevel()
      }
    },
    nextLevel (){
      Swal.fire({
        html: '<div><div>恭喜过关</div><div>本关得分: 800</div></div>',
        confirmButtonText: '进入下一关',
        confirmButtonClass: 'alertComfirm'
      }).then((result) => {
        if (result.value){
          this.level ++
          this.isInit = 'init'
          this.init()
        }
      })
    }
  }
}
</script>

<style>
.deck {
    width: 100%;
    background: linear-gradient(160deg, #02ccba 0%, #aa7ecd 100%);
    padding: 8px;
    border-radius: 10px;
    box-shadow: 12px 15px 20px 0 rgba(46, 61, 73, 0.5);
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    margin: 0 0 3em;
}
.deck .open .card{
    transform: rotateY(360deg);
    background: #02b3e4;
    cursor: default;
    transition: transform 0.3s;
}
.deck .card .icon {
	display: none;
	width: 100%;
	height: 100%;
	background-size: 100% 100%;
	background-repeat: no-repeat;
}
.deck .show .icon {
	display: block;
}
.deck .match .icon {
	display: block;
}
.deck .match .card {
    cursor: default;
    background: #02ccba;
    font-size: 33px;
    animation: fbig 0.3s alternate;
}
.swal2-styled.swal2-confirm.alertComfirm {
  background: linear-gradient(160deg, #02ccba 0%, #aa7ecd 100%);
}
</style>
