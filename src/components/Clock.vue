<template>
  <div class="clock">
    {{ time | deleteText }}
    <p v-if="display">{{ message }}</p>
  </div>
</template>

<script>
export default {
  name: "Clock",
  data() {
    return {
      display: false,
      message: "Second is 0",
      time: this.getTime(),
    };
  },

  methods: {
    getTime() {
      setInterval(() => {
        this.time = new Date().toLocaleTimeString();
      }, 1000);
    },
  },

  filters: {
    deleteText(value = " ") {
      if (value === undefined) {
        return "";
      } else {
        return value.substring(0, value.length - 3);
      }
    },
  },

  watch: {
    time(val) {
      if (val.substring(0, val.length - 3).endsWith("00") === true) {
        this.display = true;
        setTimeout(() => {
          this.display = false;
        }, 2000);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.clock {
  color: white;
  font-size: 5rem;
}
p {
  color: red;
  font-size: 2rem;
}
</style>
