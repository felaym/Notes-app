<script setup lang="ts">
import { ref, computed } from 'vue'
import NoteInput from './components/NoteInput.vue'
import NoteList from './components/NoteList.vue'

type Note = {
  id: string
  text: string
  importance: number
  createdAt: Date
}

const notes = ref<Note[]>([])

function addNote(text: string, importance: number) {
  notes.value.push({
    id: crypto.randomUUID(),
    text,
    importance,
    createdAt: new Date(),
  })
}

function removeNote(id: string) {
  notes.value = notes.value.filter((note) => note.id !== id)
}

const sortedNotes = computed(() => [...notes.value].sort((a, b) => b.importance - a.importance))
</script>

<template>
  <div class="app">
    <div class="container">
      <div class="header">
        <h1>📝 Мої нотатки</h1>
        <p class="subtitle">Додавайте та керуйте своїми нотатками</p>
      </div>

      <div class="input-container">
        <NoteInput @add="addNote" />
      </div>

      <div v-if="sortedNotes.length > 0" class="notes-container">
        <NoteList :notes="sortedNotes" @remove="removeNote" />
      </div>

      <div v-else class="empty-state">
        <p>Нотаток ще немає. Додайте першу!</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  min-height: 100vh;
  background-color: lightgray;
  padding: 2rem 1rem;
  margin: 0;
}

.container {
  max-width: 42rem;
  margin: 0 auto;
}

.header {
  text-align: center;
  margin-bottom: 2rem;
}

.header h1 {
  font-size: 1.875rem;
  font-weight: 700;
  color: #4f46e5;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
}

.subtitle {
  color: #6b7280;
  margin-top: 0.5rem;
}

.input-container,
.notes-container {
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  padding: 1.5rem;
  margin-bottom: 1.5rem;
}

.empty-state {
  text-align: center;
  padding: 3rem 0;
  background-color: white;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.empty-state p {
  color: #6b7280;
}
</style>
