<template>
  <div>
    <h2>{{ customtitle  }}</h2>
    <p>{{ counter }} <sup>2</sup>= {{ counter * counter }}</p>

    <button @click="increase">+1</button>
    <button @click="decrease">-1</button>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    start: {
        type: Number, 
        default: 100
    }
  },
  data() {
    return {
      counter: this.start,
    }
  },

  methods: {
    increase() {
      this.counter++
    },

    decrease() {
      this.counter = this.counter - 1
    },
  },

  computed: {
    customtitle() {
      return this.title || "counter"
    },
  },
}
</script>

<style></style>
