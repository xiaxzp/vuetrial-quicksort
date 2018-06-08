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
export default {
  name: 'App',
  data () { return {title: 'appss', inputdata: '1,2,3,1,4,7,2'} },
  methods: {
    buttonclk () {
      let tparray = this.inputdata.split(',').map(x => parseInt(x))
      let tparray2 = []
      tparray.map(x => tparray2.push(x))
      let time = new Date().getTime()
      console.log(qksort(tparray))
      console.log(new Date().getTime() - time)
      time = new Date().getTime()
      calcpromis(tparray2)
      console.log(new Date().getTime() - time)
    }
  }
}
function qksort (arr) {
  if (arr.length <= 1) { return arr }
  let left = []
  let right = []
  let base = [arr.pop()]
  for (let x of arr) {
    if (x <= base[0]) {
      left.push(x)
    } else {
      right.push(x)
    }
  }
  return qksort(left).concat(base, qksort(right))
}
function swap (arr, i, j) {
  if (arr[i] > arr[j]) {
    let temp = 0
    temp = arr[i]
    arr[i] = arr[j]
    arr[j] = temp
  }
}
function minheapsort (arr) {
  if (arr.length <= 1) { return arr }
  let result = []
  let times = arr.length
  for (let i = times; i > 0; i--) {
    for (let j = Math.pow(2, parseInt(Math.sqrt(arr.length))) - 2; j >= 0; j--) {
      if (((j + 1) * 2 + 1) <= arr.length) {
        if (arr[((j + 1) * 2)] < arr[((j + 1) * 2 - 1)]) {
          swap(arr, j, ((j + 1) * 2))
        } else {
          swap(arr, j, ((j + 1) * 2 - 1))
        }
      } else if (((j + 1) * 2) <= arr.length) {
        swap(arr, j, ((j + 1) * 2 - 1))
      } else {
        continue
      }
    }
    swap(arr, arr.length - 1, 0)
    result.push(arr.pop())
  }
  return result
}
function calcpromis (arr) {
  var pms = new Promise((resolve, reject) => {
    console.log(arr)
    resolve(minheapsort(arr))
    // reject(new Error('asss'))
  })
  pms.then((value) => {
    console.log(value)
  }, (reason) => {
    console.log(reason)
  })
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
