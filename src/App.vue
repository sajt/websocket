<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <h1>{{time}}</h1>
  <h2>Text color{{color}}</h2>
  <h3>Background color{{backgroundColor}}</h3>
</template>
<script>
export default {
  name: 'App',
  data() {
    return {
      time: null,
      color: 'black',
      backgroundColor: 'white'
    }
  },
  watch: {
    time() {
      try {
        let newColor = this.time.split(' ').pop().split(':')
        newColor = newColor.map((value, index) => {
          const divider = (index === 0) ? 23 : 59
          return Math.round(255 / divider * value)
        })
        let newColorInverse = newColor.map((cur) => 255 - cur)

        this.color = "rgb(" + newColor.join() + ")"
        this.backgroundColor = "rgb(" + newColorInverse.join() + ")"
      } catch (error) {
        return "#abccba"  
      }
    }
  },
  mounted() {
    setInterval(() => {
    let time = new Date();
    this.time = time.toLocaleString('hu-HU');
  }, 1000);
  }
}
</script>

<style>
h1 {
  color: v-bind(color);
  background-color: v-bind(backgroundColor);
  padding: 25px;
  border-radius: 25px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
