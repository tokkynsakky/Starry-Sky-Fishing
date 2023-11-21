<!-- App.vue -->

<template>
  <div id="app">
    <!-- <TitleScreen /> -->
    <router-view />
  </div>
</template>

<script lang="ts">
import { ref, computed, defineComponent, type DefineComponent } from "vue";
import TitleScreen from "./views/TitleScreen.vue";
import MainScreen from "./views/MainScreen.vue";
import CaptchaRocket from "./views/CaptchaRocket.vue";
import GenerateRocket from "./views/GenerateRocket.vue";

export default defineComponent({
  components: {
    TitleScreen,
  },
});

const routes: Record<string, any> = {
  "/": TitleScreen,
  "/main": MainScreen,
  "/main/captchaRocket": CaptchaRocket,
  "/main/generateRocket": GenerateRocket,
};

const currentPath = ref(window.location.hash);

window.addEventListener("hashchange", () => {
  currentPath.value = window.location.hash;
});

const currentView = computed(() => {
  return routes[currentPath.value.slice(1) || "/"];
});
</script>

<style>
/* グローバルなスタイルが必要であればここに追加 */
</style>
