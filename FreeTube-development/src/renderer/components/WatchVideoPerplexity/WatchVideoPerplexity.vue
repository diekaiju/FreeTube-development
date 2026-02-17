<template>
  <FtCard class="watchVideoSideBar watchVideoPerplexity">
    <div class="header">
      <h4>{{ $t('Perplexity AI') }}</h4>
      <button
        class="closeButton"
        @click="$emit('close')"
      >
        <font-awesome-icon :icon="['fas', 'times']" />
      </button>
    </div>
    <div class="perplexityContainer">
      <webview
        :src="perplexityUrl"
        class="perplexityFrame"
        allowpopups
      />
    </div>
  </FtCard>
</template>

<script setup>
import { computed } from 'vue'
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
import FtCard from '../ft-card/ft-card.vue'

const props = defineProps({
  videoId: {
    type: String,
    required: true
  }
})

defineEmits(['close'])

const perplexityUrl = computed(() => {
  const youtubeUrl = `https://www.youtube.com/watch?v=${props.videoId}`
  const query = `${youtubeUrl} summarise it`
  return `https://www.perplexity.ai/search/?q=${encodeURIComponent(query)}`
})
</script>

<style scoped>
.watchVideoPerplexity {
  display: flex;
  flex-direction: column;
  height: 600px; /* Default height, will be controlled by parent or flex */
  overflow: hidden;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: var(--card-bg-color);
  border-bottom: 1px solid var(--sidebar-border-color);
}

.header h4 {
  margin: 0;
  font-size: 1.1rem;
}

.closeButton {
  background: none;
  border: none;
  cursor: pointer;
  color: var(--text-color);
  font-size: 1.1rem;
}

.perplexityContainer {
  flex: 1;
  width: 100%;
  height: 100%;
  position: relative;
}

.perplexityFrame {
  width: 100%;
  height: 100%;
  border: none;
}
</style>
