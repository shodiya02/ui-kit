<template>
  <div class="min-h-screen bg-background p-8">
    <div class="max-w-2xl mx-auto space-y-8">

      <div class="space-y-4">
        <h1 class="text-2xl font-bold text-foreground">MultiSelect - Figma Aligned</h1>
      </div>

      <!-- Test different variants -->
      <div class="space-y-6">
        <div class="space-y-2">
          <label class="text-sm font-medium text-foreground">Default State</label>
          <MultiSelect
            v-model="selected1"
            :options="regionOptions"
            placeholder="Выберите область"
            display-variant="with-checkbox"
          />
        </div>

        <div class="space-y-2">
          <label class="text-sm font-medium text-foreground">Error State</label>
          <MultiSelect
            v-model="selected2"
            :options="regionOptions"
            placeholder="Выберите область"
            variant="error"
            display-variant="with-checkbox"
          />
          <p class="text-xs text-destructive">Количество не должно превышать 5т.</p>
        </div>

        <div class="space-y-2">
          <label class="text-sm font-medium text-foreground">Success State</label>
          <MultiSelect
            v-model="selected3"
            :options="regionOptions"
            placeholder="Выберите область"
            variant="success"
            display-variant="with-checkbox"
          />
          <p class="text-xs text-success">Все поля в вашей ответ зон</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MultiSelect from './components/MultiSelect.vue'

const regionOptions = [
  { value: 'samarkand', label: 'г. Самарканд' },
  { value: 'tashkent', label: 'г. Ташкент' },
  { value: 'navoi', label: 'г. Навоиган' },
  { value: 'andijan', label: 'г. Андижан' },
  { value: 'shahrisabz', label: 'г. Шахайбулак' },
  { value: 'ikra', label: 'г. Икра' },
  { value: 'kisto', label: 'г. Кисто' },
  { value: 'nukus', label: 'г. Нукус' }
]

const selected1 = ref(['tashkent'])
const selected2 = ref([])
const selected3 = ref(['samarkand', 'tashkent'])
</script>
