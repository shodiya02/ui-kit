<template>
  <div class="space-y-8 p-6">
    <!-- Fixed Columns & Header Table Example -->
    <div>
      <h3 class="text-lg font-semibold mb-4">Combined Fixed: Left-Right & Top-Bottom</h3>
      <Table height="400px" variant="scrollable" horizontal-scroll>
        <TableHeader>
          <TableRow>
            <!-- Corner cells: both top+left fixed (highest z-index) -->
            <TableHead fixed-vertical="top" fixed-horizontal="left" class="text-center">№</TableHead>
            <TableHead fixed-vertical="top" fixed-horizontal="left" fixed-offset-h="50px" class="text-center">Худуд</TableHead>
            <!-- Top-only fixed headers -->
            <TableHead fixed-vertical="top" class="text-center">Туман сони</TableHead>
            <TableHead fixed-vertical="top" class="text-center">Жами махалла</TableHead>
            <TableHead fixed-vertical="top" class="text-center">Харитада</TableHead>
            <TableHead fixed-vertical="top" class="text-center">Статистик</TableHead>
            <TableHead fixed-vertical="top" class="text-center">ХЕ томонидан</TableHead>
            <TableHead fixed-vertical="top" class="text-center">% кесим</TableHead>
            <TableHead fixed-vertical="top" class="text-center">Шахсий</TableHead>
            <TableHead fixed-vertical="top" class="text-center">Ижарада</TableHead>
          </TableRow>
        </TableHeader>
        <TableBody>
          <template v-for="i in 20" :key="i">
            <TableRow>
              <!-- Left-only fixed columns -->
              <TableCell fixed-horizontal="left" class="text-center">{{ i }}</TableCell>
              <TableCell fixed-horizontal="left" fixed-offset-h="50px">Регион {{ i }}</TableCell>
              <!-- Regular scrollable cells -->
              <TableCell class="text-center">{{ 10 + i }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 1000).toFixed(0) }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 800).toFixed(0) }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 500000).toFixed(0) }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 600000).toFixed(0) }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 10 + 90).toFixed(1) }}%</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 10000).toFixed(0) }}</TableCell>
              <TableCell class="text-right">{{ (Math.random() * 1000).toFixed(0) }}</TableCell>
            </TableRow>
          </template>
        </TableBody>
        <TableFooter>
          <!-- Footer row with corner cells: both bottom+left fixed -->
          <TableRow class="font-semibold bg-gray-100">
            <TableCell fixed-vertical="bottom" fixed-horizontal="left" class="text-center">Жами:</TableCell>
            <TableCell fixed-vertical="bottom" fixed-horizontal="left" fixed-offset-h="50px">Барча</TableCell>
            <!-- Bottom-only fixed totals -->
            <TableCell fixed-vertical="bottom" class="text-right">200</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">15,428</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">12,850</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">8,500,000</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">7,200,000</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">95.5%</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">125,000</TableCell>
            <TableCell fixed-vertical="bottom" class="text-right">18,500</TableCell>
          </TableRow>
        </TableFooter>
      </Table>
    </div>

    <!-- Default Table - Exact Match from Image -->
<!--    <div>-->
<!--      <Table variant="default" >-->
<!--        <TableHeader>-->
<!--          <TableRow>-->
<!--            <TableHead rowspan="2" class="align-middle text-center border-r">№</TableHead>-->
<!--            <TableHead rowspan="2" class="align-middle text-center border-r">Худуд</TableHead>-->
<!--            <TableHead rowspan="2" class="align-middle text-center border-r">Туман, Шахар сони</TableHead>-->
<!--            <TableHead colspan="2" class="text-center border-r border-b">Махаллалар</TableHead>-->
<!--            <TableHead colspan="3" class="text-center border-r border-b">Хонадонлар сон</TableHead>-->
<!--            <TableHead colspan="2" class="text-center border-r border-b">Шундан</TableHead>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableHead class="text-center border-r">Жами сони</TableHead>-->
<!--            <TableHead class="text-center border-r">Шундан харитада чизилган</TableHead>-->
<!--            <TableHead class="text-center border-r">Статистик маълумотлар бўйича</TableHead>-->
<!--            <TableHead class="text-center border-r">ХЕ гомонидан урганилган</TableHead>-->
<!--            <TableHead class="text-center border-r">% кесимида</TableHead>-->
<!--            <TableHead class="text-center border-r">Шахсий</TableHead>-->
<!--            <TableHead class="text-center">Ижарада</TableHead>-->
<!--          </TableRow>-->
<!--        </TableHeader>-->
<!--        <TableBody>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">1</TableCell>-->
<!--            <TableCell class="border-r">Андижон</TableCell>-->
<!--            <TableCell class="text-center border-r">17</TableCell>-->
<!--            <TableCell class="text-right border-r">405</TableCell>-->
<!--            <TableCell class="text-right border-r">304</TableCell>-->
<!--            <TableCell class="text-right border-r">298 213</TableCell>-->
<!--            <TableCell class="text-right border-r">234 107</TableCell>-->
<!--            <TableCell class="text-right border-r">101.2 %</TableCell>-->
<!--            <TableCell class="text-right border-r">9 845</TableCell>-->
<!--            <TableCell class="text-right">290</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">2</TableCell>-->
<!--            <TableCell class="border-r">Наманган</TableCell>-->
<!--            <TableCell class="text-center border-r">16</TableCell>-->
<!--            <TableCell class="text-right border-r">911</TableCell>-->
<!--            <TableCell class="text-right border-r">876</TableCell>-->
<!--            <TableCell class="text-right border-r">345 203</TableCell>-->
<!--            <TableCell class="text-right border-r">459 028</TableCell>-->
<!--            <TableCell class="text-right border-r">103.1 %</TableCell>-->
<!--            <TableCell class="text-right border-r">3 145</TableCell>-->
<!--            <TableCell class="text-right">546</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">4</TableCell>-->
<!--            <TableCell class="border-r">Фаргона</TableCell>-->
<!--            <TableCell class="text-center border-r">13</TableCell>-->
<!--            <TableCell class="text-right border-r">874</TableCell>-->
<!--            <TableCell class="text-right border-r">567</TableCell>-->
<!--            <TableCell class="text-right border-r">320 083</TableCell>-->
<!--            <TableCell class="text-right border-r">425 793</TableCell>-->
<!--            <TableCell class="text-right border-r">98.0 %</TableCell>-->
<!--            <TableCell class="text-right border-r">3 459</TableCell>-->
<!--            <TableCell class="text-right">978</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">3</TableCell>-->
<!--            <TableCell class="border-r">Жиззах</TableCell>-->
<!--            <TableCell class="text-center border-r">13</TableCell>-->
<!--            <TableCell class="text-right border-r">865</TableCell>-->
<!--            <TableCell class="text-right border-r">813</TableCell>-->
<!--            <TableCell class="text-right border-r">428 084</TableCell>-->
<!--            <TableCell class="text-right border-r">546 789</TableCell>-->
<!--            <TableCell class="text-right border-r">96.8 %</TableCell>-->
<!--            <TableCell class="text-right border-r">7 129</TableCell>-->
<!--            <TableCell class="text-right">678</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">4</TableCell>-->
<!--            <TableCell class="border-r">Сирдарё</TableCell>-->
<!--            <TableCell class="text-center border-r">12</TableCell>-->
<!--            <TableCell class="text-right border-r">487</TableCell>-->
<!--            <TableCell class="text-right border-r">423</TableCell>-->
<!--            <TableCell class="text-right border-r">542 214</TableCell>-->
<!--            <TableCell class="text-right border-r">189 763</TableCell>-->
<!--            <TableCell class="text-right border-r">105.5 %</TableCell>-->
<!--            <TableCell class="text-right border-r">9 786</TableCell>-->
<!--            <TableCell class="text-right">124</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">5</TableCell>-->
<!--            <TableCell class="border-r">Самарканд</TableCell>-->
<!--            <TableCell class="text-center border-r">11</TableCell>-->
<!--            <TableCell class="text-right border-r">678</TableCell>-->
<!--            <TableCell class="text-right border-r">611</TableCell>-->
<!--            <TableCell class="text-right border-r">876 428</TableCell>-->
<!--            <TableCell class="text-right border-r">243 508</TableCell>-->
<!--            <TableCell class="text-right border-r">100.1 %</TableCell>-->
<!--            <TableCell class="text-right border-r">1 567</TableCell>-->
<!--            <TableCell class="text-right">187</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">6</TableCell>-->
<!--            <TableCell class="border-r">Навои</TableCell>-->
<!--            <TableCell class="text-center border-r">16</TableCell>-->
<!--            <TableCell class="text-right border-r">488</TableCell>-->
<!--            <TableCell class="text-right border-r">398</TableCell>-->
<!--            <TableCell class="text-right border-r">420 829</TableCell>-->
<!--            <TableCell class="text-right border-r">892 743</TableCell>-->
<!--            <TableCell class="text-right border-r">93.1 %</TableCell>-->
<!--            <TableCell class="text-right border-r">2 789</TableCell>-->
<!--            <TableCell class="text-right">823</TableCell>-->
<!--          </TableRow>-->
<!--          <TableRow>-->
<!--            <TableCell class="text-center border-r">7</TableCell>-->
<!--            <TableCell class="border-r">Тошкент</TableCell>-->
<!--            <TableCell class="text-center border-r">10</TableCell>-->
<!--            <TableCell class="text-right border-r">914</TableCell>-->
<!--            <TableCell class="text-right border-r">875</TableCell>-->
<!--            <TableCell class="text-right border-r">980 231</TableCell>-->
<!--            <TableCell class="text-right border-r">342 578</TableCell>-->
<!--            <TableCell class="text-right border-r">95.9 %</TableCell>-->
<!--            <TableCell class="text-right border-r">8 564</TableCell>-->
<!--            <TableCell class="text-right">981</TableCell>-->
<!--          </TableRow>-->
<!--          &lt;!&ndash; Total Row &ndash;&gt;-->
<!--          <TableRow class="font-semibold bg-gray-100">-->
<!--            <TableCell  class="border-r">Жами:</TableCell>-->
<!--            <TableCell class="border-r"></TableCell>-->
<!--            <TableCell class="text-right border-r">124</TableCell>-->
<!--            <TableCell class="text-right border-r">982 213</TableCell>-->
<!--            <TableCell class="text-right border-r">765 927</TableCell>-->
<!--            <TableCell class="text-right border-r">12 458 084</TableCell>-->
<!--            <TableCell class="text-right border-r">5 827 211</TableCell>-->
<!--            <TableCell class="text-right border-r">97.1%</TableCell>-->
<!--            <TableCell class="text-right border-r">368 919</TableCell>-->
<!--            <TableCell class="text-right">21 089</TableCell>-->
<!--          </TableRow>-->
<!--        </TableBody>-->
<!--      </Table>-->
<!--    </div>-->

<!--    &lt;!&ndash; Scrollable Table &ndash;&gt;-->
<!--    <div>-->
<!--      <h3 class="text-lg font-semibold mb-4">Scrollable Table</h3>-->
<!--      <Table height="400px" variant="scrollable">-->
<!--        <TableHeader sticky>-->
<!--          <TableRow>-->
<!--            <TableHead>ID</TableHead>-->
<!--            <TableHead>Product</TableHead>-->
<!--            <TableHead>Category</TableHead>-->
<!--            <TableHead align="right">Price</TableHead>-->
<!--            <TableHead align="center">Stock</TableHead>-->
<!--            <TableHead align="center">Status</TableHead>-->
<!--          </TableRow>-->
<!--        </TableHeader>-->
<!--        <TableBody>-->
<!--          <template v-for="i in 50" :key="i">-->
<!--            <TableRow>-->
<!--              <TableCell>{{ i }}</TableCell>-->
<!--              <TableCell>Product {{ i }}</TableCell>-->
<!--              <TableCell>Category {{ (i % 5) + 1 }}</TableCell>-->
<!--              <TableCell align="right">${{ (Math.random() * 1000).toFixed(2) }}</TableCell>-->
<!--              <TableCell align="center">{{ Math.floor(Math.random() * 100) }}</TableCell>-->
<!--              <TableCell align="center">-->
<!--                <span :class="Math.random() > 0.5 ? 'text-green-600' : 'text-red-600'">-->
<!--                  {{ Math.random() > 0.5 ? 'In Stock' : 'Out of Stock' }}-->
<!--                </span>-->
<!--              </TableCell>-->
<!--            </TableRow>-->
<!--          </template>-->
<!--        </TableBody>-->
<!--      </Table>-->
<!--    </div>-->
  </div>
</template>

<script setup>
import {
  Table,
  TableBody,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
  TableFooter,
} from '@/components/ui/table'
</script>
