<template>
  <header>
    <nav class="row">
      <button @click="changeTab(1)" class="col-4 text-center btn btn-active" :class="active1 ? 'active' : ''">Step
        1</button>
      <button @click="changeTab(2)" class="col-4 text-center btn btn-active" :class="active2 ? 'active' : ''">Step
        2</button>
      <button @click="changeTab(3)" class="col-4 text-center btn btn-active"
        :class="active3 ? 'active' : (active2 ? '' : 'disabled')">Step
        3</button>
    </nav>
  </header>
  <TheWelcome :active1="active1" :active2="active2" :active3="active3" />
</template>

<script>
import TheWelcome from './components/TheWelcome.vue'
export default {
  props: ["active1", "active2", "active3"],
  components: {
    'TheWelcome': TheWelcome,
  },
  data() {
    return {
      active1: true,
      active2: false,
      active3: false,
    }
  },
  methods: {
    changeTab(active) {
      this.active1 = active == 1 ? true : false;
      this.active2 = active == 2 ? true : false;
      this.active3 = active == 3 ? true : false;
    }
  }
}
</script>

<style>
.active {
  background: #e7f2f8;
}
</style>
