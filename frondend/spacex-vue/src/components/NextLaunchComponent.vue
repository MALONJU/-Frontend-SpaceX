<template>
  <div class="card mb-4">
    <div class="card-body">
      <h2 class="card-title">Prochain lancement</h2>
      <div v-if="launch">
        <p><strong>Nom :</strong> {{ launch.name }}</p>
        <p><strong>Date :</strong> {{ formattedDate }}</p>
        <p><strong>Décompte :</strong> {{ countdown }} secondes</p>
      </div>
      <div v-else>
        <div class="spinner-border text-primary" role="status">
          <span class="visually-hidden">Chargement...</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted, onUnmounted, computed } from 'vue'
import axios from 'axios'

export default defineComponent({
  name: 'NextLaunchComponent',
  setup() {
    const launch = ref(null)
    const countdown = ref(0)
    let interval

    const fetchNextLaunch = async () => {
      const res = await axios.get('https://api.spacexdata.com/v5/launches/next')
      launch.value = res.data
      updateCountdown()
    }

    const updateCountdown = () => {
      if (!launch.value) return
      const launchDate = new Date(launch.value.date_utc).getTime()
      const now = Date.now()
      countdown.value = Math.max(0, Math.floor((launchDate - now) / 1000))
    }

    onMounted(() => {
      fetchNextLaunch()
      interval = setInterval(updateCountdown, 1000)
    })

    onUnmounted(() => {
      clearInterval(interval)
    })

    const formattedDate = computed(() =>
      launch.value ? new Date(launch.value.date_utc).toLocaleString('fr-FR') : ''
    )

    return {
      launch,
      countdown,
      formattedDate
    }
  }
})
</script>