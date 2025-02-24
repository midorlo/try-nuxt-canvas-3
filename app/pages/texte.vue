<template>
  <div class="card-container">
    <div
      v-for="(text, index) in texts"
      :key="index"
      class="card"
      @mouseover="isHovered = index"
      @mouseleave="isHovered = null"
    >
      <div class="card-content">
        <h3>{{ text.title }}</h3>
        <p v-html="text.body"></p>
      </div>
      <button class="copy-button" @click="copyToClipboard(text.body)">Copy</button>
    </div>
  </div>
</template>

<script setup>
const texts = await queryContent('texte').find();

const copyToClipboard = (text) => {
  navigator.clipboard.writeText(text).then(() => {
    alert('Text kopiert!');
  });
};
</script>

<style scoped>
.card-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.card {
  background-color: white;
  border-radius: 8px;
  padding: 16px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: relative;
  overflow: hidden;
  transition: transform 0.3s ease;
}

.card:hover {
  transform: translateY(-5px);
}

.card-content {
  max-height: 150px;
  overflow: hidden;
  position: relative;
}

.card-content:hover {
  max-height: none;
  overflow-y: scroll;
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
