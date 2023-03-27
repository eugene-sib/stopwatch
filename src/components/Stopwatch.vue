<script setup>
import { ref, computed } from "vue";

const timer = ref(false);
const count = ref(0);

const formatTime = computed(() => {
  const seconds = Math.floor((count.value / 100) % 60);
  const minutes = Math.floor((count.value / 100 / 60) % 60);
  const hours = Math.floor((count.value / 100 / 60 / 60) % 24);

  return [
    hours.toString().padStart(2, "0"),
    minutes.toString().padStart(2, "0"),
    seconds.toString().padStart(2, "0"),
  ].join(":");
});

function start() {
  if (!timer.value) {
    timer.value = true;
    fire();
  }
}

function pause() {
  timer.value = false;
}

function reset() {
  timer.value = false;
  count.value = 0;
}

function fire() {
  if (timer.value) {
    count.value++;
    setTimeout(fire, 10);
  }
}
</script>

<template>
  <article :class="{ active: timer }" class="stopwatch">
    <div class="stopwatch__time">
      {{ formatTime }}
    </div>
    <div class="stopwatch__controls controls">
      <button
        type="button"
        v-on="{ click: timer ? pause : start }"
        class="controls__button">
        <svg
          v-if="!timer"
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24">
          <path d="M3 22v-20l18 10-18 10z" />
        </svg>
        <svg
          v-else
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24">
          <path d="M11 22h-4v-20h4v20zm6-20h-4v20h4v-20z" />
        </svg>
      </button>
      <button type="button" @click="reset" class="controls__button">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="24"
          height="24"
          viewBox="0 0 24 24">
          <path d="M2 2h20v20h-20z" />
        </svg>
      </button>
    </div>
  </article>
</template>

<style lang="scss" scoped>
.stopwatch {
  display: flex;
  flex-direction: column;

  width: 225px;
  height: 120px;

  background-color: #696969;

  &__time {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 100%;
    height: 100%;
    color: #9e9e9e;

    text-align: center;
    vertical-align: middle;
    font-size: 22px;

    border-bottom: 1px solid #9e9e9e;
  }

  &__controls {
    display: flex;
    justify-content: space-evenly;
    align-items: center;

    width: 100%;
    height: 100%;

    & svg {
      fill: #9e9e9e;
    }
  }
}

.active {
  & .stopwatch__time {
    color: #fff;
    border-color: #fff;
  }

  & .stopwatch__controls svg {
    fill: #fff;
  }
}
</style>
