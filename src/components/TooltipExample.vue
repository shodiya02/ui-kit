<template>
  <TooltipProvider>
    <div class="space-y-12 p-8">
      <!-- Header -->
      <div>
        <h2 class="text-2xl font-bold mb-2">Tooltip Examples</h2>
        <p class="text-gray-600">Hover over the buttons to see tooltips in different positions</p>
      </div>

      <!-- Basic Tooltip Positions -->
      <div class="space-y-8">
        <h3 class="text-xl font-semibold">Basic Positions</h3>
        
        <div class="grid grid-cols-4 gap-8 max-w-2xl">
          <!-- Top -->
          <div class="flex flex-col items-center space-y-4">
            <h4 class="font-medium text-gray-700">top</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                  Текст
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <p>Андижон</p>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Bottom -->
          <div class="flex flex-col items-center space-y-4">
            <h4 class="font-medium text-gray-700">bottom</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <div class="text-center space-y-2">
                  <div class="text-sm text-gray-600">Андижон</div>
                  <div class="relative inline-block">
                    <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                      Текст
                    </button>
                    <div class="absolute top-0 left-1/2 transform -translate-x-1/2 -translate-y-2">
                      <div class="w-0 h-0 border-l-4 border-r-4 border-b-4 border-transparent border-b-blue-600"></div>
                    </div>
                  </div>
                </div>
              </TooltipTrigger>
              <TooltipContent side="bottom">
                <p>Андижон</p>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Right -->
          <div class="flex flex-col items-center space-y-4">
            <h4 class="font-medium text-gray-700">right</h4>
            <div class="flex items-center space-x-2">
              <div class="text-center">
                <div class="text-sm mb-1">a</div>
                <Tooltip>
                  <TooltipTrigger as-child>
                    <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                      Текст
                    </button>
                  </TooltipTrigger>
                  <TooltipContent side="right">
                    <p>Андижон</p>
                  </TooltipContent>
                </Tooltip>
                <div class="text-sm mt-1">c</div>
              </div>
              <div class="text-center">
                <div class="text-sm mb-1">b</div>
                <div class="h-10 w-8"></div>
                <div class="text-sm mt-1">c</div>
              </div>
            </div>
          </div>

          <!-- Left -->
          <div class="flex flex-col items-center space-y-4">
            <h4 class="font-medium text-gray-700">left</h4>
            <div class="flex items-center space-x-2">
              <div class="text-center">
                <div class="text-sm mb-1">a</div>
                <div class="h-10 w-8"></div>
                <div class="text-sm mt-1">c</div>
              </div>
              <div class="text-center">
                <div class="text-sm mb-1">b</div>
                <Tooltip>
                  <TooltipTrigger as-child>
                    <button class="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors">
                      Текст
                    </button>
                  </TooltipTrigger>
                  <TooltipContent side="left">
                    <p>Андижон</p>
                  </TooltipContent>
                </Tooltip>
                <div class="text-sm mt-1">c</div>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Advanced Examples -->
      <div class="space-y-8">
        <h3 class="text-xl font-semibold">Advanced Examples</h3>
        
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <!-- Multi-line tooltip -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Multi-line Content</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-green-600 text-white rounded-lg hover:bg-green-700 transition-colors">
                  Hover for details
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <div class="space-y-1">
                  <p class="font-semibold">User Information</p>
                  <p>Name: John Doe</p>
                  <p>Status: Active</p>
                  <p>Last login: 2 hours ago</p>
                </div>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Icon with tooltip -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Icon Tooltip</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <button class="p-2 rounded-full bg-gray-200 hover:bg-gray-300 transition-colors">
                  <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                  </svg>
                </button>
              </TooltipTrigger>
              <TooltipContent side="right">
                <p>Click for more information</p>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Action buttons with tooltips -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Action Buttons</h4>
            <div class="flex space-x-2">
              <Tooltip>
                <TooltipTrigger as-child>
                  <button class="p-2 rounded bg-blue-600 text-white hover:bg-blue-700 transition-colors">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M11 5H6a2 2 0 00-2 2v11a2 2 0 002 2h11a2 2 0 002-2v-5m-1.414-9.414a2 2 0 112.828 2.828L11.828 15H9v-2.828l8.586-8.586z"></path>
                    </svg>
                  </button>
                </TooltipTrigger>
                <TooltipContent side="top">
                  <p>Edit item</p>
                </TooltipContent>
              </Tooltip>
              
              <Tooltip>
                <TooltipTrigger as-child>
                  <button class="p-2 rounded bg-red-600 text-white hover:bg-red-700 transition-colors">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                    </svg>
                  </button>
                </TooltipTrigger>
                <TooltipContent side="top">
                  <p>Delete item</p>
                </TooltipContent>
              </Tooltip>
              
              <Tooltip>
                <TooltipTrigger as-child>
                  <button class="p-2 rounded bg-green-600 text-white hover:bg-green-700 transition-colors">
                    <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                      <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 4v16m8-8H4"></path>
                    </svg>
                  </button>
                </TooltipTrigger>
                <TooltipContent side="top">
                  <p>Add new item</p>
                </TooltipContent>
              </Tooltip>
            </div>
          </div>

          <!-- Disabled state -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Disabled Button</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <button 
                  disabled
                  class="px-4 py-2 bg-gray-300 text-gray-500 rounded-lg cursor-not-allowed"
                >
                  Disabled
                </button>
              </TooltipTrigger>
              <TooltipContent side="bottom">
                <p>This action is currently unavailable</p>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Text element with tooltip -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Text Element</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <span class="text-blue-600 underline cursor-pointer hover:text-blue-800">
                  Hover over this text
                </span>
              </TooltipTrigger>
              <TooltipContent side="right">
                <p>Additional context for this text</p>
              </TooltipContent>
            </Tooltip>
          </div>

          <!-- Long content -->
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Long Content</h4>
            <Tooltip>
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                  Long tooltip
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <div class="max-w-xs">
                  <p class="font-semibold mb-2">Detailed Information</p>
                  <p>This is a longer tooltip that contains more detailed information about the element you're hovering over. It automatically wraps to multiple lines when the content is too long.</p>
                </div>
              </TooltipContent>
            </Tooltip>
          </div>
        </div>
      </div>

      <!-- Custom Delays -->
      <div class="space-y-8">
        <h3 class="text-xl font-semibold">Custom Timing</h3>
        
        <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Fast (100ms)</h4>
            <Tooltip :delay-duration="100">
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-orange-600 text-white rounded-lg hover:bg-orange-700 transition-colors">
                  Fast tooltip
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <p>This tooltip appears quickly</p>
              </TooltipContent>
            </Tooltip>
          </div>
          
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Normal (700ms)</h4>
            <Tooltip :delay-duration="700">
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-teal-600 text-white rounded-lg hover:bg-teal-700 transition-colors">
                  Normal tooltip
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <p>Default timing</p>
              </TooltipContent>
            </Tooltip>
          </div>
          
          <div class="space-y-2">
            <h4 class="font-medium text-gray-700">Slow (1500ms)</h4>
            <Tooltip :delay-duration="1500">
              <TooltipTrigger as-child>
                <button class="px-4 py-2 bg-pink-600 text-white rounded-lg hover:bg-pink-700 transition-colors">
                  Slow tooltip
                </button>
              </TooltipTrigger>
              <TooltipContent side="top">
                <p>This tooltip takes longer to appear</p>
              </TooltipContent>
            </Tooltip>
          </div>
        </div>
      </div>
    </div>
  </TooltipProvider>
</template>

<script setup>
import {
  Tooltip,
  TooltipContent,
  TooltipProvider,
  TooltipTrigger,
} from '@/components/ui/tooltip'
</script>