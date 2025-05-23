<template>
  <div class="card shadow-lg mb-4 border-primary">
    <div class="card-header bg-primary text-white">
      <h2 class="card-title mb-0">🚀 Prochain lancement</h2>
    </div>
    <div class="card-body">
      <div v-if="launch">
        <ul class="list-group list-group-flush mb-3">
          <li class="list-group-item">
            <strong>Nom :</strong>
            <span class="text-primary ms-2">{{ launch.name }}</span>
          </li>
          <li class="list-group-item">
            <strong>Date :</strong>
            <span class="ms-2">{{ formattedDate }}</span>
          </li>
          <li class="list-group-item">
            <strong>Décompte :</strong>
            <span class="badge bg-success ms-2 fs-5">{{ countdown }}</span>
            <span class="ms-1">secondes</span>
          </li>
        </ul>
        <div v-if="launch.links?.patch?.small" class="text-center">
          <img :src="launch.links.patch.small" alt="Mission patch" class="img-fluid" style="max-height:80px;" />
        </div>
      </div>
      <div v-else>
        <div class="d-flex flex-column align-items-center py-4">
          <div class="spinner-border text-primary mb-2" role="status">
            <span class="visually-hidden">Chargement...</span>
          </div>
          <span>Chargement du prochain lancement...</span>
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
      launch.value ? new Date(launch.value.date_utc).toLocaleString('fr-FR', { dateStyle: 'full', timeStyle: 'short' }) : ''
    )

    return {
      launch,
      countdown,
      formattedDate
    }
  }
})
</script>