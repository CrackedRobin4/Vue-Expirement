<template>
  <h1 v-bind:title="message"> Hello. Here's your task of the day</h1>
  <button @click="start">Start</button>
  <div class="non-active" v-bind:class="{active: isActive}">
    <h3>Solve this problem</h3>
    <h4>Timer</h4>
    <p>{{ timer }}</p>
    <div>
      <span>{{ random1 }} + {{ random2 }} = </span>
      <span><input type="text" id="answer"></span>
    </div>
    <button @click="check">Submit</button>
    <div>
      <p class="non-active" v-bind:class="{correct: isCorrect}">You are correct</p>
      <p class="non-active" v-bind:class="{notCorrect: isNotCorrect}">You are not correct</p>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return{
      isActive: false,
      isCorrect: false,
      isNotCorrect: false,
      message: 'Hello World',
      timer: 10,
      random1: 0,
      random2: 0
    }
  },
  methods: {
    start(){
      document.getElementById("answer").value = ""
      this.timer = 10
      this.isActive = true
      this.isCorrect = false;
      this.isNotCorrect = false;
      this.random1 = Math.floor(Math.random() * 1000) + 1
      this.random2 = Math.floor(Math.random() * 1000) + 1
      let timerID = setInterval(() => {
        this.timer--
      }, 1000);
      setTimeout(() => { clearInterval(timerID); this.isActive = false;}, 10000);
    },
    check(){
      if(document.getElementById("answer").value == (this.random1 + this.random2)){
        this.isNotCorrect = false
        this.isCorrect = true
      }
      else{
        this.isCorrect = false
        this.isNotCorrect = true
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
button {
  margin: 50px;
  margin-bottom: 20px;
  width: 200px;
  height: 100px;
}
input {
  width: 70px;
}
.non-active {
  display: none;
}
.active {
  display: block;
}
.correct {
  color: green;
  display: block;
}
.notCorrect{
  color: red;
  display: block;
}
</style>
