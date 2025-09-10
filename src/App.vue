<template>
  <div class="min-h-screen p-8">
    <div class="max-w-2xl mx-auto space-y-8">
      <div class="space-y-4">
        <h1 class="text-2xl font-bold text-foreground">MultiSelect - Figma Aligned</h1>
      </div>

      <TooltipExample/>
      <TableExample />

      <!-- Test different variants -->
<!--      <div class="space-y-6">-->
<!--        <div class="space-y-2">-->
<!--          <MultiSelect-->
<!--            v-model="selected1"-->
<!--            :options="regionOptions"-->
<!--            display-variant="with-checkbox"-->
<!--            label="Выберите область"-->
<!--          />-->
<!--        </div>-->
<!--      </div>-->
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MultiSelect from './components/MultiSelect.vue'
import TableExample from '@/components/TableExample.vue'
import TooltipExample from '@/components/TooltipExample.vue'

const regionOptions = [
  { value: 'samarkand', label: 'г. Самарканд' },
  { value: 'tashkent', label: 'г. Ташкент' },
  { value: 'navoi', label: 'г. Навоиган' },
  { value: 'andijan', label: 'г. Андижан' },
  { value: 'shahrisabz', label: 'г. Шахайбулак' },
  { value: 'ikra', label: 'г. Икра' },
  { value: 'kisto', label: 'г. Кисто' },
  { value: 'nukus', label: 'г. Нукус' },
]

const selected1 = ref(['tashkent'])
const selected2 = ref([])
const selected3 = ref(['samarkand', 'tashkent'])
</script>
