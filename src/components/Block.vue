<template>
  <div class="block" v-show="showBlock" @click="stopTimer">
    click me
  </div>
</template>

<script>
export default {
  props: ['delay'],
  data() {
    return {
      showBlock: false,
      timer: null,
      reactionTime: 0
    }
  },
  methods: {
    startTimer() {
      // start the timer, tick every 10ms
      this.timer = setInterval(() => {
        this.reactionTime += 10
      }, 10)
    },
    stopTimer() {
      // stop the timer
      clearInterval(this.timer)
      this.$emit('end', this.reactionTime)
    }
  },
  beforeCreate() {
    console.log("beforeCreate: The component is not created yet.");
  },
  created() {
    console.log("created: The component just got created.");
  },
  beforeMount() {
    console.log("beforeMount: This is just before the component is mounted.");
  },
  mounted() {
    console.log("mounted: This is just after the component is mounted.");
    setTimeout(() => {
      this.showBlock = true
      this.startTimer()
    }, this.delay)
  },
  beforeUpdate() {
    console.log("beforeUpdate: This happened just before the 'updated' hook.");
  },
  updated() {
    console.log("updated: This is just after the component is updated.");
  },
  beforeUnmount() {
    console.log("beforeUnmount: reaction time: ", this.reactionTime);
  },
  unmounted() {
    console.log("unmounted: The component is removed");
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.block {
  width: 400px;
  border-radius: 20px;
  background: #0faf87;
  color: white;
  text-align: center;
  padding: 100px 0;
  margin: 40px auto;
}
</style>