<script setup>
import sourceData from '@/data.json'
import ExperienceCard from '@/components/ExperienceCard.vue'
import { computed } from 'vue'
import GoBack from '@/components/GoBack.vue'
const props = defineProps({
  id: { type: Number, required: true }
})
const destination = computed(() =>
  sourceData.destinations.find((destination) => destination.id === props.id)
)
// DADOS VIA AJAX MODIFICAR TAMBÉM App.vue
// let destination = ref(null)
// onMounted(async () => {
//   const resp = await fetch(
//     `https://travel-dummy-api.netlify.app/${route.params.slug}`
//   )
//   destination.value = await resp.json()
// })
</script>

<template>
  <div>
    <section v-if="destination" class="destination">
      <h1>{{ destination.name }}</h1>
      <GoBack />
      <div class="destination-details">
        <img :src="`/images/${destination.image}`" :alt="destination.name" />
        <p>{{ destination.description }}</p>
      </div>
    </section>
    <section class="experiences">
      <h2>Tope Experiences in {{ destination.name }}</h2>
      <div class="cards">
        <RouterLink
          v-for="experience in destination.experiences"
          :key="experience.slug"
          :to="{
            name: 'experience.show',
            params: { experienceSlug: experience.slug }
          }"
        >
          <ExperienceCard :experience="experience" />
        </RouterLink>
      </div>
      <RouterView />
    </section>
  </div>
</template>
