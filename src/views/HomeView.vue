<script setup>
import sourceData from '@/data.json'
import { useRouter, isNavigationFailure, NavigationFailureType } from 'vue-router'
const router = useRouter()
const destinations = sourceData.destinations
const triggerRouterError = async () => {
  const navigationFailure = await router.push('/')
  if (isNavigationFailure(navigationFailure, NavigationFailureType.duplicated)) {
    console.log(navigationFailure.to)
    console.log(navigationFailure.from)
  }
}
const addDynamicRoute = () => {
  const removeDynamicRoute = router.addRoute({
    name: 'dynamic',
    path: '/dynamic',
    component: () => import('@/views/Login.vue')
  })
  // PARA REMOVER A ROTA CRIADA
  // removeDynamicRoute() ou router.removeRoute('dynamic')
}
</script>

<template>
  <div class="home">
    <h1>All Destinations</h1>
    <button @click="triggerRouterError">Trigger Router Error</button>
    <button @click="addDynamicRoute">Add Dynamic Route</button>
    <AppLink to="/dynamic">Visit Dynamic Route</AppLink>
    <div class="destinations">
      <RouterLink
        v-for="destination in destinations"
        :key="destination.id"
        :to="{
          name: 'destination.show',
          params: { id: destination.id, slug: destination.slug }
        }"
      >
        <h2>{{ destination.name }}</h2>
        <img :src="`/images/${destination.image}`" :alt="destination.name" />
      </RouterLink>
    </div>
  </div>
</template>
