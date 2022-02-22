<template>

  <div>

    <button class="activate" v-if="!started && (!displayFirst && !displaySecond)" v-on:click="startRoutine()">Start Activity</button>

    <img v-if="displayFirst" src="./assets/HackOne.gif" alt="keycard loading">
    <img v-else-if="displaySecond" src="./assets/HackSecond.png" alt="stolen keycard">

    <button class="return" v-if="started" v-on:click="started = !started">Return</button>
    <Activity v-if="started" />
    
  </div>
</template>

<script>

import Activity from './components/Activity.vue'

export default {
  name: 'App',
  components: {
    Activity
  },
  data: () => {
    return {
      started: false,
      displayFirst: false,
      displaySecond: false,
    }
  },
  methods: {
    startRoutine() {
      this.displayFirst = true;
      setTimeout(() => {
        this.displayFirst = false;
        this.displaySecond = true;
      }, 2000)
      setTimeout(() => {
        this.displaySecond = false;
        this.started = !this.started;
      }, 3000)
    }
  }
}
</script>

<style>
  button {
    background-color: gray;
    color: white;
    border-radius: 5px;
    padding: 1% 5% 1% 5%;
    font-weight: bold;
    font-size: 15pt;  
    border: 2px solid black;
  }
  button.activate {
    margin-top: 45vh;
  }
  button:hover {
    background-color: royalblue;
    cursor: pointer;
  }
  div {
    display: flex;
    align-items: center;
    align-content: center;
    justify-content: center;
    flex-direction: column;
  }
  div.main-menu {
    margin-top: 10vh;
    border: 2px solid white;
    padding: 15%;
    background-color: rgb(49, 80, 175);
  }
  html {
    background-color: #232531; 
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  }
  input {
    margin-top: 10vh;
    background-color: white;
    width: 50vh;
    font-size: 14pt;
    height: 5vh;
    font-weight: bold;
    padding: 0px 10px 0px 10px;
    border-radius: 10px;
    border: 2px solid black;
  }
  .numbers-display {
    color: white;
  }
  button.return {
    background-color: lightcoral;
    font-size: 10pt;
    padding: .5%;
  }
  button.return:hover {
    background-color: red;
    cursor: pointer;
    border-radius: 25px;
    
  }
  img {
    width: 80vw;
    height: 80vh;
    object-fit: cover;
  }
</style>
