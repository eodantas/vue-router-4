<script setup>
import Navigation from '@/components/TheNavigation.vue'
import { useRoute } from 'vue-router'
const route = useRoute()
</script>

<template>
  <Navigation />
  <div class="container">
    <RouterView v-slot="{ Component }" class="view left-sidebar" name="LeftSidebar">
      <Transition name="fade" mode="out-in">
        <Component :is="Component" :key="route.path"></Component>
      </Transition>
    </RouterView>
    <!-- USAR QDO OS DADOS VIEREM DE CHAMADA AJAX -->
    <!-- <RouterView :key="route.path" /> -->
    <RouterView v-slot="{ Component }" class="main-view">
      <!-- <Transition name="slide" mode="out-in"> -->
      <Transition name="fade" mode="out-in">
        <Component :is="Component" :key="route.path"></Component>
      </Transition>
    </RouterView>
  </div>
</template>

<style lang="css">
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
.slide-enter-active,
.slide-leave-active {
  transition: opacity 1s, transform 1s;
}
.slide-enter-from,
.slide-leave-to {
  opacity: 0;
  transform: translateX(-30%);
}
.moveUp-enter-active {
  animation: fadeIn 1s ease-in;
}
@keyframes fadeIn {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 0.5;
  }
  100% {
    opacity: 1;
  }
}
.moveUp-leave-active {
  animation: moveUp 0.3s ease-in;
}
@keyframes moveUp {
  0% {
    transform: translateY(0);
  }
  100% {
    transform: translateY(-400px);
  }
}
.main-view {
  width: 100%;
}
</style>
