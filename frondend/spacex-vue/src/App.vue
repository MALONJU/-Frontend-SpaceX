<template>
  <div class="container mt-4">
    <h1 class="text-center mb-4">SpaceX Launches</h1>
    <NextLaunchComponent />
    <LaunchListComponent />
  </div>
</template>

<script>
import { defineComponent } from 'vue'
import NextLaunchComponent from './components/NextLaunchComponent.vue'
import LaunchListComponent from './components/LaunchListComponent.vue'

export default defineComponent({
  name: 'App',
  components: {
    NextLaunchComponent,
    LaunchListComponent
  }
})
</script>