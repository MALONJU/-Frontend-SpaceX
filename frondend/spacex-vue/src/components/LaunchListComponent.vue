<template>
  <div class="card mb-4">
    <div class="card-body">
      <label for="filter" class="form-label fw-bold">Filtrer les lancements :</label>
      <select id="filter" class="form-select mb-3" v-model="filter" @change="fetchLaunches">
        <option value="all">Tous les lancements</option>
        <option value="success">Lancements réussis</option>
        <option value="fail">Lancements échoués</option>
      </select>
      <ul class="list-group mb-3">
        <li
          v-for="launch in launches"
          :key="launch.id"
          class="list-group-item list-group-item-action d-flex justify-content-between align-items-center"
          @click="selectLaunch(launch)"
          style="cursor:pointer"
        >
          <span>
            <span class="fw-bold">{{ launch.name }}</span>
            <span class="text-muted ms-2">{{ new Date(launch.date_utc).toLocaleDateString('fr-FR') }}</span>
          </span>
          <span>
            <span v-if="launch.success === true" class="badge bg-success">Succès</span>
            <span v-else-if="launch.success === false" class="badge bg-danger">Échec</span>
            <span v-else class="badge bg-secondary">À venir</span>
          </span>
        </li>
      </ul>
      <div v-if="loading" class="mt-3 text-center">
        <div class="spinner-border text-primary" role="status">
          <span class="visually-hidden">Chargement...</span>
        </div>
      </div>
      <LaunchModalComponent
        v-if="selectedLaunch"
        :launch="selectedLaunch"
        @close="selectedLaunch = null"
      />
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, onMounted } from 'vue'
import axios from 'axios'
import LaunchModalComponent from './LaunchModalComponent.vue'

export default defineComponent({
  name: 'LaunchListComponent',
  components: { LaunchModalComponent },
  setup() {
    const filter = ref('all')
    const launches = ref([])
    const loading = ref(false)
    const selectedLaunch = ref(null)

    const fetchLaunches = async () => {
      loading.value = true
      let query = {}
      if (filter.value === 'success') query.success = true
      if (filter.value === 'fail') query.success = false

      const res = await axios.post('https://api.spacexdata.com/v5/launches/query', {
        query,
        options: { sort: { date_utc: 'desc' }, limit: 10 }
      })
      launches.value = res.data.docs
      loading.value = false
    }

    const selectLaunch = (launch) => {
      selectedLaunch.value = launch
    }

    onMounted(fetchLaunches)

    return {
      filter,
      launches,
      loading,
      selectedLaunch,
      fetchLaunches,
      selectLaunch
    }
  }
})
</script>