<template>
    <div>

        
        <div v-if="attempting" class="main-menu">
            <h2>Successful Attempts: {{ successfulAttempts }}/12</h2>
            <h2>Attempts Remaining: {{ attempts }}/3</h2>
            <h1 clas="numbers-display">Your Password Is:</h1>
            <h1 class="numbers-display">{{ display }}</h1> 
            <input ref="input" v-model="input" type="number" v-on:keyup.enter="validate()" />
            <button class="validation">Time Remaining: {{ time }}</button>
        </div>
        
        <div v-else>
            <h1 style="color: limegreen; margin-top: 40vh;">
                You Hacked Flecca Bank Successfully!
            </h1>
        </div>

    </div>
   
</template>

<script>
export default {
    data: () => {
    return {
        attempting: true,
        input: "",
        numbers: 0,
        display: "",
        time: 5,
        attempts: 3,
        successfulAttempts: 0,
    }
  },
  
  created() {
    this.timeTracker = setInterval(() => {
        this.time--;
    }, 1000)
  },
  destroyed() {
    clearInterval(this.timeTracker);
  },
  watch: {
      attempts() {
          if (this.attempts === 0) {
              location.reload();
          }
      },
      successfulAttempts() {
          if (this.successfulAttempts === 12) {
              clearInterval(this.timeTracker);
              this.attempts += 100;
              this.attempting = false;
          }
      },
      time() {
          if (this.time === 0) {
              this.attempts--;
              this.time = 5;
              this.input = "";
              this.start();
          }
      }
  },
  methods: {
    start() {
      let newNumber = Math.random() * 1000000;
      this.numbers = Math.round(newNumber);
      this.numbers = String(this.numbers);
      while (this.numbers.length < 6) {  
        this.numbers = '0' + this.numbers;
      }
      this.display = this.numbers;
      setTimeout(() => this.display = 'XXXXXX', 650);
    },
    validate() {
        if (this.input == this.numbers) {
            this.successfulAttempts++;
        } else {
            this.attempts--;
        }
        
        this.input = "";
        this.time = 5;
        this.start();
    }
  },
  mounted() {
    this.$refs.input.focus();
    this.start();
  }
}
</script>

<style  scoped>
    h2 {
        color: white;
        font-size: 10pt;
    }
    .validation {
        background-color: white;
        color: black;
        margin-top: 5vh;
        border: 2px solid black; 
    }
    .validation:hover {
        background-color: khaki;
        cursor: default;
    }
    h1 {
        color: white;
    }
    h1.output {
        font-size: 10pt;
        margin: 1vh;
    }
</style>
