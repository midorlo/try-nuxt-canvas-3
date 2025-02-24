<template>
  <div class="card" @mouseover="isHovered = true" @mouseleave="isHovered = false">
    <div class="card-content" :class="{ 'hovered': isHovered }">
      <nuxt-content :document="document" />
    </div>
    <button class="copy-button" @click="copyToClipboard">Copy</button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const props = defineProps({
  document: Object
});

const isHovered = ref(false);

const copyToClipboard = () => {
  navigator.clipboard.writeText(props.document.body).then(() => {
    alert('Text copied to clipboard!');
  });
};
</script>

<style scoped>
.card {
  background-color: white;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease;
  max-width: 300px; /* Anpassung für die Sidebar */
}

.card:hover {
  transform: translateY(-5px);
}

.card-content {
  max-height: 150px;
  overflow: hidden;
  position: relative;
}

.card-content.hovered {
  max-height: none;
  overflow-y: auto;
}

.card-content::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 0;
  width: 100%;
  height: 30px;
  background: linear-gradient(to top, white, transparent);
  pointer-events: none;
}

.copy-button {
  position: absolute;
  top: 8px;
  right: 8px;
  background: #007bff;
  color: white;
  border: none;
  padding: 8px 12px;
  border-radius: 4px;
  cursor: pointer;
}

.copy-button:hover {
  background: #0056b3;
}
</style>
