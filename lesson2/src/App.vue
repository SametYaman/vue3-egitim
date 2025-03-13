<script setup>
import { ref } from 'vue'

// Reaktif değişkenler
const title = ref('Vue 3 Temel Direktifler')
const isVisible = ref(true)
const count = ref(0)

// Liste örneği için veri
const fruits = ref([
  { id: 1, name: 'Elma', color: 'red' },
  { id: 2, name: 'Muz', color: 'yellow' },
  { id: 3, name: 'Üzüm', color: 'purple' }
])

// v-model için form değişkenleri
const username = ref('')
const selectedFruit = ref('')
const message = ref('')
const isSubscribed = ref(false)

// Metodlar
const toggleVisibility = () => {
  isVisible.value = !isVisible.value
}

const incrementCount = () => {
  count.value++
}

const addFruit = () => {
  fruits.value.push({
    id: fruits.value.length + 1,
    name: 'Yeni Meyve',
    color: 'green'
  })
}

const submitForm = () => {
  alert(`Form Bilgileri:
    Kullanıcı Adı: ${username.value}
    Seçilen Meyve: ${selectedFruit.value}
    Mesaj: ${message.value}
    Abonelik: ${isSubscribed.value}
  `)
}
</script>

<template>
  <div class="container">
    <!-- v-bind örneği -->
    <h1 :class="{ 'title': true, 'hidden': !isVisible }">
      {{ title }}
    </h1>

    <!-- v-if ve v-show örnekleri -->
    <div class="example-section">
      <h2>v-if ve v-show Örnekleri</h2>
      <p v-if="isVisible">Bu metin v-if ile kontrol ediliyor</p>
      <p v-show="isVisible">Bu metin v-show ile kontrol ediliyor</p>
      <button @click="toggleVisibility">Görünürlüğü Değiştir</button>
    </div>

    <!-- v-on örneği -->
    <div class="example-section">
      <h2>v-on (@) Örneği</h2>
      <p>Sayaç: {{ count }}</p>
      <button @click="incrementCount">Artır</button>
    </div>

    <!-- v-for örneği -->
    <div class="example-section">
      <h2>v-for Örneği</h2>
      <ul>
        <li v-for="fruit in fruits" :key="fruit.id">
          <span :style="{ color: fruit.color }">{{ fruit.name }}</span>
        </li>
      </ul>
      <button @click="addFruit">Yeni Meyve Ekle</button>
    </div>

    <!-- v-model örneği -->
    <div class="example-section">
      <h2>v-model Örneği (Form Elemanları)</h2>
      <form @submit.prevent="submitForm" class="form-group">
        <!-- Text input -->
        <div class="form-item">
          <label>Kullanıcı Adı:</label>
          <input type="text" v-model="username" placeholder="Adınızı girin">
          <p class="preview">Girilen değer: {{ username }}</p>
        </div>

        <!-- Select -->
        <div class="form-item">
          <label>Favori Meyveniz:</label>
          <select v-model="selectedFruit">
            <option value="">Seçiniz...</option>
            <option v-for="fruit in fruits" :key="fruit.id" :value="fruit.name">
              {{ fruit.name }}
            </option>
          </select>
          <p class="preview">Seçilen meyve: {{ selectedFruit }}</p>
        </div>

        <!-- Textarea -->
        <div class="form-item">
          <label>Mesajınız:</label>
          <textarea v-model="message" placeholder="Mesajınızı yazın"></textarea>
          <p class="preview">Mesaj uzunluğu: {{ message.length }} karakter</p>
        </div>

        <!-- Checkbox -->
        <div class="form-item">
          <label class="checkbox-label">
            <input type="checkbox" v-model="isSubscribed">
            Haberlere abone ol
          </label>
          <p class="preview">Abonelik durumu: {{ isSubscribed ? 'Evet' : 'Hayır' }}</p>
        </div>

        <button type="submit">Formu Gönder</button>
      </form>
    </div>
  </div>
</template>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
}

.example-section {
  margin: 20px 0;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

.title {
  color: #42b883;
  transition: opacity 0.3s;
}

.hidden {
  opacity: 0.5;
}

button {
  background-color: #42b883;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  cursor: pointer;
  margin: 5px;
}

button:hover {
  background-color: #3aa876;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  margin: 5px 0;
  padding: 5px;
  background-color: #f5f5f5;
  border-radius: 4px;
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.form-item {
  display: flex;
  flex-direction: column;
  gap: 5px;
}

.form-item label {
  font-weight: bold;
  color: #2c3e50;
}

.form-item input[type="text"],
.form-item select,
.form-item textarea {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 14px;
}

.form-item textarea {
  min-height: 100px;
  resize: vertical;
}

.checkbox-label {
  display: flex;
  align-items: center;
  gap: 8px;
}

.preview {
  font-size: 14px;
  color: #666;
  margin: 5px 0;
  font-style: italic;
}
</style>
