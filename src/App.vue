<script setup>
import { ref } from "vue";
import Stopwatch from "./components/Stopwatch.vue";

const stopwatches = ref([{ name: "Stopwatch" }]);

function addStopwatch() {
  stopwatches.value.push({ name: "Stopwatch" });
}
</script>

<template>
  <section class="stopwatches">
    <div v-for="(stopwatch, index) in stopwatches" :key="index">
      <component :key="index" :is="Stopwatch"></component>
    </div>
    <button type="button" @click="addStopwatch()" class="btn btn-add">
      <svg
        width="40px"
        height="40px"
        clip-rule="evenodd"
        fill-rule="evenodd"
        stroke-linejoin="round"
        stroke-miterlimit="2"
        viewBox="0 0 24 24"
        fill="#9E9E9E"
        xmlns="http://www.w3.org/2000/svg">
        <path
          d="m11 11h-7.25c-.414 0-.75.336-.75.75s.336.75.75.75h7.25v7.25c0 .414.336.75.75.75s.75-.336.75-.75v-7.25h7.25c.414 0 .75-.336.75-.75s-.336-.75-.75-.75h-7.25v-7.25c0-.414-.336-.75-.75-.75s-.75.336-.75.75z"
          fill-rule="nonzero" />
      </svg>
    </button>
  </section>
</template>

<style lang="scss" scoped>
.stopwatches {
  display: grid;
  gap: 3em;

  grid-template-columns: repeat(auto-fill, 225px);

  margin-inline: auto;

  max-width: 775px;

  @media only screen and (max-width: 800px) {
    max-width: 500px;
  }

  @media only screen and (max-width: 514px) {
    max-width: 225px;
  }
}
.btn-add {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 225px;
  height: 120px;
}
</style>
