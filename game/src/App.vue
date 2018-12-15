<template>
  <div id="app">
    <ul class="ullist">
    <li v-for="(i,k) in arr" :key="k" v-if="i==''" class="active">{{i}}</li>
    <li v-else @click="changeli(k)">{{i}}</li>
    </ul>
    <button class="btn" @click="reject">重置游戏</button>
    <button class="btn1" @click="resole">一键还原</button>
  </div>
</template>

<script>
import game from './game/game.vue'
export default {
  name: 'App',
  components: {
    game
  },
  mounted () {
    this.changes()
  },
  methods: {
    reject () {
      this.changes()
    },
    changes () {
      this.arr = new Array(15)
        .fill(0)
        .map((v, i) => i + 1)
        .sort(() => 0.5 - Math.random())
        .filter((v, i) => i < 15)
      this.arr = this.arr.concat([''])
      this.default = 15
    },
    changeli (k) {
      if (k === this.default - 1 || k === this.default + 1 || k === this.default - 4 || k === this.default + 4) {
        this.arr[this.default] = this.arr[k]
        this.$set(this.arr, k, '')
        this.default = k
      }
    },
    resole () {
      this.arr = new Array(15)
      for (let i = 1; i <= 15; i++) {
        this.arr[i - 1] = i
      }
      this.arr = this.arr.concat([''])
    }
  },
  data () {
    return {
      arr: [],
      default: 15
    }
  }
}
</script>

<style>
#app{
  text-align: center;
}
*{
  margin: 0;
  padding: 0;
}
.ullist{
  width: 400px;
  height: 400px;
  list-style: none;
  margin: 0;
}
.ullist li{
  display: inline-block;
  width: 23%;
  height: 23%;
  border:1px solid #ccc;
  text-align: center;
  line-height: 100px;
  overflow: hidden;
  margin: 0 2px;
  background: orange;
}
.active{
  background: rgb(121, 115, 115)!important;
}
.btn{
  width: 200px;
  height: 50px;
  border-radius: 15px;
  border:0;
  background: orange;
  color: white;

}
.btn{
  width: 200px;
  height: 50px;
  border-radius: 15px;
  border:0;
  background: orange;
  color: white;

}
</style>
