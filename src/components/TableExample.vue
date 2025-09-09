<template>
  <div class="space-y-8 p-6">
    <!-- Default Table -->
    <div>
      <h3 class="text-lg font-semibold mb-4">Default Table</h3>
      <Table>
        <TableHeader>
          <TableRow>
            <TableHead>№</TableHead>
            <TableHead>Name</TableHead>
            <TableHead align="right">Amount</TableHead>
            <TableHead align="center">Status</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <TableRow>
            <TableCell>1</TableCell>
            <TableCell>John Doe</TableCell>
            <TableCell align="right">$250.00</TableCell>
            <TableCell align="center">Active</TableCell>
          </TableRow>
          <TableRow>
            <TableCell>2</TableCell>
            <TableCell>Jane Smith</TableCell>
            <TableCell align="right">$150.00</TableCell>
            <TableCell align="center">Inactive</TableCell>
          </TableRow>
        </TableBody>
      </Table>
    </div>

    <!-- Fixed Header Table with Title -->
    <div>
      <h3 class="text-lg font-semibold mb-4">Fixed Header Table with Title</h3>
      <Table variant="fixed" title="Таблица - Fixed" height="300px">
        <TableHeader sticky>
          <TableRow>
            <TableHead>№</TableHead>
            <TableHead>Худуд</TableHead>
            <TableHead>Умум. Ҷахон сони</TableHead>
            <TableHead>Жами сони</TableHead>
            <TableHead>Шуладан </TableHead>
            <TableHead>Статистик </TableHead>
            <TableHead>ХЕ гомонидан ургаништан</TableHead>
            <TableHead>У кеси</TableHead>
            <TableHead>Шахсий</TableHead>
            <TableHead>Ижарада</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <TableRow variant="striped">
            <TableCell>1</TableCell>
            <TableCell>Андижон</TableCell>
            <TableCell align="right">17</TableCell>
            <TableCell align="right">405</TableCell>
            <TableCell align="right">304</TableCell>
            <TableCell align="right">298 213</TableCell>
            <TableCell align="right">234 107</TableCell>
            <TableCell align="right">101</TableCell>
            <TableCell align="right">9 845</TableCell>
            <TableCell align="right">290</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>2</TableCell>
            <TableCell>Наманган</TableCell>
            <TableCell align="right">16</TableCell>
            <TableCell align="right">911</TableCell>
            <TableCell align="right">876</TableCell>
            <TableCell align="right">345 203</TableCell>
            <TableCell align="right">459 028</TableCell>
            <TableCell align="right">103</TableCell>
            <TableCell align="right">3 145</TableCell>
            <TableCell align="right">546</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>3</TableCell>
            <TableCell>Фарғона</TableCell>
            <TableCell align="right">13</TableCell>
            <TableCell align="right">874</TableCell>
            <TableCell align="right">567</TableCell>
            <TableCell align="right">320 083</TableCell>
            <TableCell align="right">425 793</TableCell>
            <TableCell align="right">98</TableCell>
            <TableCell align="right">3 459</TableCell>
            <TableCell align="right">978</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>4</TableCell>
            <TableCell>Жиззах</TableCell>
            <TableCell align="right">13</TableCell>
            <TableCell align="right">865</TableCell>
            <TableCell align="right">813</TableCell>
            <TableCell align="right">428 084</TableCell>
            <TableCell align="right">546 789</TableCell>
            <TableCell align="right">96</TableCell>
            <TableCell align="right">7 129</TableCell>
            <TableCell align="right">678</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>5</TableCell>
            <TableCell>Сирдарё</TableCell>
            <TableCell align="right">12</TableCell>
            <TableCell align="right">487</TableCell>
            <TableCell align="right">423</TableCell>
            <TableCell align="right">542 214</TableCell>
            <TableCell align="right">189 763</TableCell>
            <TableCell align="right">105</TableCell>
            <TableCell align="right">9 786</TableCell>
            <TableCell align="right">124</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>6</TableCell>
            <TableCell>Самарқанд</TableCell>
            <TableCell align="right">11</TableCell>
            <TableCell align="right">678</TableCell>
            <TableCell align="right">611</TableCell>
            <TableCell align="right">876 428</TableCell>
            <TableCell align="right">243 508</TableCell>
            <TableCell align="right">100</TableCell>
            <TableCell align="right">1 567</TableCell>
            <TableCell align="right">187</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>7</TableCell>
            <TableCell>Навои</TableCell>
            <TableCell align="right">16</TableCell>
            <TableCell align="right">488</TableCell>
            <TableCell align="right">398</TableCell>
            <TableCell align="right">420 829</TableCell>
            <TableCell align="right">892 743</TableCell>
            <TableCell align="right">93</TableCell>
            <TableCell align="right">2 789</TableCell>
            <TableCell align="right">823</TableCell>
          </TableRow>
          <TableRow variant="striped">
            <TableCell>8</TableCell>
            <TableCell>Тошкент</TableCell>
            <TableCell align="right">10</TableCell>
            <TableCell align="right">914</TableCell>
            <TableCell align="right">875</TableCell>
            <TableCell align="right">980 231</TableCell>
            <TableCell align="right">342 578</TableCell>
            <TableCell align="right">95</TableCell>
            <TableCell align="right">8 564</TableCell>
            <TableCell align="right">981</TableCell>
          </TableRow>
          <!-- Total Row -->
          <TableRow class="font-semibold bg-gray-100">
            <TableCell>Жами:</TableCell>
            <TableCell>8 вилоят</TableCell>
            <TableCell align="right">124</TableCell>
            <TableCell align="right">982 213</TableCell>
            <TableCell align="right">765 927</TableCell>
            <TableCell align="right">12 458 084</TableCell>
            <TableCell align="right">5 827 211</TableCell>
            <TableCell align="right">97</TableCell>
            <TableCell align="right">368 919</TableCell>
            <TableCell align="right">21 089</TableCell>
          </TableRow>
        </TableBody>
      </Table>
    </div>

    <!-- Scrollable Table -->
    <div>
      <h3 class="text-lg font-semibold mb-4">Scrollable Table</h3>
      <Table variant="scrollable" height="400px">
        <TableHeader sticky>
          <TableRow>
            <TableHead>ID</TableHead>
            <TableHead>Product</TableHead>
            <TableHead>Category</TableHead>
            <TableHead align="right">Price</TableHead>
            <TableHead align="center">Stock</TableHead>
            <TableHead align="center">Status</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <template v-for="i in 50" :key="i">
            <TableRow>
              <TableCell>{{ i }}</TableCell>
              <TableCell>Product {{ i }}</TableCell>
              <TableCell>Category {{ (i % 5) + 1 }}</TableCell>
              <TableCell align="right">${{ (Math.random() * 1000).toFixed(2) }}</TableCell>
              <TableCell align="center">{{ Math.floor(Math.random() * 100) }}</TableCell>
              <TableCell align="center">
                <span :class="Math.random() > 0.5 ? 'text-green-600' : 'text-red-600'">
                  {{ Math.random() > 0.5 ? 'In Stock' : 'Out of Stock' }}
                </span>
              </TableCell>
            </TableRow>
          </template>
        </TableBody>
      </Table>
    </div>

    <!-- Fixed Columns Table -->
    <div>
      <h3 class="text-lg font-semibold mb-4">Fixed Columns Table (Left & Right)</h3>
      <Table variant="scrollable" height="400px" horizontal-scroll>
        <TableHeader sticky>
          <TableRow>
            <TableHead fixed="left" fixed-offset="0px" class="min-w-[60px] w-[60px]">ID</TableHead>
            <TableHead fixed="left" fixed-offset="60px" class="min-w-[120px] w-[120px]">Company</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Q1 Sales</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Q2 Sales</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Q3 Sales</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Q4 Sales</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Marketing</TableHead>
            <TableHead class="min-w-[120px] w-[120px]">Operations</TableHead>
            <TableHead fixed="right" fixed-offset="80px" align="right" class="min-w-[100px] w-[100px]">Revenue</TableHead>
            <TableHead fixed="right" fixed-offset="0px" align="center" class="min-w-[80px] w-[80px]">Status</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <template v-for="company in dynamicTableData" :key="company.id">
            <TableRow>
              <TableCell fixed="left" fixed-offset="0px" class="min-w-[60px] w-[60px]">{{ company.id }}</TableCell>
              <TableCell fixed="left" fixed-offset="60px" class="min-w-[120px] w-[120px] font-medium">{{ company.name }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.q1Sales.toLocaleString() }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.q2Sales.toLocaleString() }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.q3Sales.toLocaleString() }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.q4Sales.toLocaleString() }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.marketing.toLocaleString() }}</TableCell>
              <TableCell class="min-w-[120px] w-[120px]">${{ company.operations.toLocaleString() }}</TableCell>
              <TableCell fixed="right" fixed-offset="80px" align="right" class="min-w-[100px] w-[100px] font-semibold">
                ${{ company.totalRevenue.toLocaleString() }}
              </TableCell>
              <TableCell fixed="right" fixed-offset="0px" align="center" class="min-w-[80px] w-[80px]">
                <span 
                  :class="[
                    'px-2 py-1 rounded-full text-xs font-medium',
                    company.status === 'Active' ? 'bg-green-100 text-green-800' :
                    company.status === 'Pending' ? 'bg-yellow-100 text-yellow-800' :
                    'bg-red-100 text-red-800'
                  ]"
                >
                  {{ company.status }}
                </span>
              </TableCell>
            </TableRow>
          </template>
        </TableBody>
      </Table>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import {
  Table,
  TableHeader,
  TableBody,
  TableHead,
  TableRow,
  TableCell,
} from '@/components/ui/table'

// Dynamic table data
const companies = [
  'TechCorp Solutions', 'Global Innovations', 'DataFlow Systems', 'CloudMax Enterprise',
  'InnovateTech', 'FutureSoft', 'NextGen Analytics', 'SmartBiz Solutions',
  'DigitalEdge', 'ProActive Systems', 'MetaData Inc', 'CyberLink Technologies',
  'WebForce Dynamics', 'AI Ventures', 'BlockChain Innovations', 'QuantumLeap',
  'ByteStream Corp', 'CodeCrafters', 'TechVision Group', 'DataMine Solutions'
]

const statuses = ['Active', 'Pending', 'Inactive']

const generateRandomData = (id) => {
  const q1 = Math.floor(Math.random() * 500000) + 100000
  const q2 = Math.floor(Math.random() * 600000) + 150000
  const q3 = Math.floor(Math.random() * 550000) + 120000
  const q4 = Math.floor(Math.random() * 700000) + 200000
  const marketing = Math.floor(Math.random() * 100000) + 20000
  const operations = Math.floor(Math.random() * 80000) + 15000
  
  return {
    id,
    name: companies[id - 1] || `Company ${id}`,
    q1Sales: q1,
    q2Sales: q2,
    q3Sales: q3,
    q4Sales: q4,
    marketing,
    operations,
    totalRevenue: q1 + q2 + q3 + q4,
    status: statuses[Math.floor(Math.random() * statuses.length)]
  }
}

const dynamicTableData = ref(
  Array.from({ length: 25 }, (_, index) => generateRandomData(index + 1))
)
</script>
