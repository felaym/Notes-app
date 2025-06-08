<script setup lang="ts">
import { ref } from 'vue'

const newNote = ref('')
const importance = ref(3)

const emit = defineEmits<{
  (e: 'add', text: string, importance: number): void
}>()

function submit() {
  if (newNote.value.trim()) {
    emit('add', newNote.value.trim(), importance.value)
    newNote.value = ''
    importance.value = 3
  }
}
</script>

<template>
  <div class="note-input">
    <h2>Додати нову нотатку</h2>
    <div class="input-group">
      <input
        v-model="newNote"
        placeholder="Введіть текст нотатки..."
        @keyup.enter="submit"
      />
      <select v-model="importance">
        <option v-for="i in 5" :key="i" :value="i">{{ i }}</option>
      </select>
      <button @click="submit">
        Додати
      </button>
    </div>
  </div>
</template>

<style scoped>
.note-input h2 {
  font-size: 1.125rem;
  font-weight: 500;
  color: #374151;
  margin-bottom: 1rem;
}

.input-group {
  display: flex;
  gap: 0.5rem;
}

.input-group input {
  flex: 1;
  padding: 0.5rem 1rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  font-size: 1rem;
  outline: none;
  transition: all 0.2s;
}

.input-group input:focus {
  border-color: #4f46e5;
  box-shadow: 0 0 0 2px rgba(79, 70, 229, 0.2);
}

.input-group select {
  padding: 0.5rem;
  border: 1px solid #d1d5db;
  border-radius: 0.375rem;
  outline: none;
  transition: all 0.2s;
}

.input-group select:focus {
  border-color: #4f46e5;
  box-shadow: 0 0 0 2px rgba(79, 70, 229, 0.2);
}

.input-group button {
  padding: 0.5rem 1rem;
  background-color: #4f46e5;
  color: white;
  border: none;
  border-radius: 0.375rem;
  font-weight: 500;
  cursor: pointer;
  transition: background-color 0.2s;
}

.input-group button:hover {
  background-color: #4338ca;
}
</style>
