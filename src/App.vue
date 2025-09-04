<template>
  <div class="min-h-screen bg-background p-8">
    <div class="max-w-2xl mx-auto space-y-8">

      <div class="space-y-4">
        <h1 class="text-3xl font-bold text-foreground">Professional UI Kit</h1>
        <p class="text-muted-foreground">Testing integrated theming system</p>
      </div>

      <!-- shadcn-vue buttons using your brand colors automatically -->
      <div class="space-y-4">
        <h2 class="text-xl font-semibold">shadcn-vue Buttons (Auto-themed)</h2>
        <div class="flex gap-4 flex-wrap">
          <Button>Primary Button</Button>
          <Button variant="secondary">Secondary Button</Button>
          <Button variant="destructive">Destructive Button</Button>
          <Button variant="outline">Outline Button</Button>
        </div>
      </div>

      <!-- Your MultiSelect with integrated theming -->
      <div class="space-y-4">
        <h2 class="text-xl font-semibold">Multi-Select Component</h2>
        <MultiSelect
          v-model="selectedRegions"
          :options="regionOptions"
          placeholder="Выберите область"
        />

        <MultiSelect
          v-model="selectedError"
          :options="regionOptions"
          placeholder="Error state"
          variant="error"
        />
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { Button } from '@/components/ui/button'
import MultiSelect from './components/MultiSelect.vue'

const regionOptions = [
  { value: 'tashkent', label: 'г. Ташкент' },
  { value: 'samarkand', label: 'г. Самарканд' },
  { value: 'navoi', label: 'г. Навоиган' },
  { value: 'andijan', label: 'г. Андижан' }
]

const selectedRegions = ref(['tashkent'])
const selectedError = ref([])
</script>
