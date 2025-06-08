<script setup lang="ts">
import NoteItem from './NoteItem.vue'

type Note = {
  id: string
  text: string
  importance: number
  createdAt: Date
}

const props = defineProps<{
  notes: Note[]
}>()

const emit = defineEmits<{
  (e: 'remove', id: string): void
}>()
</script>

<template>
  <div class="note-list">
    <h2>Список нотаток</h2>
    <ul>
      <li v-for="note in notes" :key="note.id" class="note-item">
        <NoteItem :note="note" />
        <button @click="emit('remove', note.id)" class="delete-btn" title="Видалити">❌</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.note-list h2 {
  font-size: 1.25rem;
  font-weight: 600;
  color: #374151;
  margin-bottom: 1rem;
}

.note-list ul {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
}

.note-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1rem;
  border: 1px solid #e5e7eb;
  border-radius: 0.5rem;
  transition: background-color 0.2s;
}

.note-item:hover {
  background-color: #f9fafb;
}

.delete-btn {
  padding: 0.5rem;
  color: #6b7280;
  border-radius: 50%;
  transition: all 0.2s;
}

.delete-btn:hover {
  color: #ef4444;
  background-color: #fee2e2;
}
</style>
