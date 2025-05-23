<template>
  <div class="modal fade show d-block" tabindex="-1" style="background:rgba(0,0,0,0.5)">
    <div class="modal-dialog modal-lg">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title">{{ launch.name }}</h5>
          <button type="button" class="btn-close" @click="$emit('close')"></button>
        </div>
        <div class="modal-body">
          <p><strong>Date :</strong> {{ formattedDate }}</p>
          <p><strong>Détails :</strong> {{ launch.details || 'Aucun détail.' }}</p>
          <div class="text-center mb-3">
            <img v-if="launch.links?.patch?.small" :src="launch.links.patch.small" class="img-fluid" style="max-height:100px;" />
          </div>
          <div v-if="launch.links?.article">
            <a :href="launch.links.article" target="_blank" class="btn btn-outline-primary btn-sm mb-2">Voir l'article</a>
          </div>
          <div class="form-check form-switch my-2">
            <input class="form-check-input" type="checkbox" v-model="showVideo" id="videoSwitch">
            <label class="form-check-label" for="videoSwitch">Afficher la vidéo YouTube</label>
          </div>
          <div v-if="showVideo && launch.links?.youtube_id" class="mb-3">
            <iframe
              width="100%"
              height="315"
              :src="`https://www.youtube.com/embed/${launch.links.youtube_id}`"
              frameborder="0"
              allowfullscreen
            ></iframe>
          </div>
          <p><strong>Lieu de lancement :</strong> {{ launch.launchpad }}</p>
          <p><strong>Payloads :</strong> {{ launch.payloads?.join(', ') }}</p>
          <!-- Pour afficher les clients, il faudrait charger les détails des payloads -->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent, ref, computed } from 'vue'

export default defineComponent({
  name: 'LaunchModalComponent',
  props: {
    launch: { type: Object, required: true }
  },
  setup(props) {
    const showVideo = ref(false)
    const formattedDate = computed(() =>
      props.launch.date_utc ? new Date(props.launch.date_utc).toLocaleDateString('fr-FR', { dateStyle: 'full', timeStyle: 'short' }) : ''
    )
    return { showVideo, formattedDate }
  }
})
</script>