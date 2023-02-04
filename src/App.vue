<template>
  <div>
    <button v-on:click="toggle1">과제1 보기</button>
    <button v-on:click="toggle2">과제2 보기</button>

    <Assign1 v-if="show1" />
    <Assign2 v-if="show2" />
  </div>
</template>
<script>
import Assign1 from "./components/Assign1.vue";
import Assign2 from "./components/Assign2.vue";

export default {
  created() {},
  components: {
    Assign1,
    Assign2,
  },
  data() {
    return {
      show1: false,
      show2: true,
    };
  },
  methods: {
    toggle1: function () {
      this.show1 = !this.show1;
    },
    toggle2: function () {
      this.show2 = !this.show2;
    },
  },
};
</script>
<style scoped></style>
