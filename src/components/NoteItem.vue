<script setup lang="ts">
defineProps<{
  note: {
    id: string
    text: string
    importance: number
    createdAt: Date
  }
}>()

const formatDate = (date: Date) => {
  return new Intl.DateTimeFormat('uk-UA', {
    day: '2-digit',
    month: '2-digit',
    year: 'numeric',
    hour: '2-digit',
    minute: '2-digit',
  }).format(date)
}

const getImportanceColor = (importance: number) => {
  if (importance <= 2) return 'green'
  if (importance === 3) return 'orange'
  return 'red'
}
</script>

<template>
  <div class="note-content">
    <p class="note-text">{{ note.text }}</p>
    <div class="note-meta">
      <div class="importance" :class="getImportanceColor(note.importance)">
        <span>Важливість:</span>
        <span class="value">{{ note.importance }}</span>
        <div class="dots">
          <span v-for="i in 5" :key="i" :class="{ active: i <= note.importance }" />
        </div>
      </div>
      <span class="separator">•</span>
      <span class="date">{{ formatDate(note.createdAt) }}</span>
    </div>
  </div>
</template>

<style scoped>
.note-content {
  flex: 1;
}

.note-text {
  color: #374151;
  margin-bottom: 0.25rem;
}

.note-meta {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 0.875rem;
  color: #6b7280;
}

.importance {
  display: flex;
  align-items: center;
  gap: 0.25rem;
}

.importance.green .value {
  color: #10b981;
  font-weight: 500;
}

.importance.orange .value {
  color: #f59e0b;
  font-weight: 500;
}

.importance.red .value {
  color: #ef4444;
  font-weight: 500;
}

.dots {
  display: flex;
  gap: 0.125rem;
}

.dots span {
  width: 0.5rem;
  height: 0.5rem;
  border-radius: 50%;
  background-color: #e5e7eb;
}

.dots span.active {
  background-color: currentColor;
}

.importance.green .dots span.active {
  background-color: #10b981;
}

.importance.orange .dots span.active {
  background-color: #f59e0b;
}

.importance.red .dots span.active {
  background-color: #ef4444;
}

.separator {
  opacity: 0.5;
}
</style>
