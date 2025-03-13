<script setup>

const message = 'Merhaba Vue 3!'
</script>

<template>
  <div class="container">
    <h1>{{ message }}</h1>
    <p>Bu benim ilk Vue 3 uygulamam!</p>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

h1 {
  color: #42b883;
}
</style>
