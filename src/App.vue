<template>
  <div id="app">
    {{ title }}
    <img src="./assets/logo.png">
    <router-view/>
    <textarea id="inputbox" v-model="inputdata" style="width: 400px;height: 100px;"></textarea>
    <input type="button" id="input-button" @click="buttonclk()" value="button">
  </div>
</template>

<script>
let count = 0
export default {
  name: 'App',
  data () { return {title: 'appss', inputdata: '1,2,3'} },
  methods: {
    buttonclk () {
      let tparray = this.inputdata.split(',').map(x => parseInt(x))
      console.log(qksort(tparray))
      console.log(count)
    }
  }
}
function qksort (arr) {
  if (arr.length <= 1) { return arr }
  count += 1
  let left = []
  let right = []
  let base = [arr.pop()]
  for (let x of arr) {
    if (x <= base[0]) {
      left.push(x)
    }
    else {
      right.push(x)
    }
  }
  return qksort(left).concat(base, qksort(right))
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
