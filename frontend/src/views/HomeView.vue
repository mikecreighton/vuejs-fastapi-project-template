<script setup>
import { ref } from "vue"
import { Button } from '@/components/ui/button'
import { DropdownMenu, DropdownMenuContent, DropdownMenuItem, DropdownMenuTrigger } from '@/components/ui/dropdown-menu'
import { Icon } from '@iconify/vue'
import { useColorMode } from '@vueuse/core'

// Pass { disableTransition: false } to enable transitions
const mode = useColorMode({
  disableTransition: false
})

const handleSayHello = async () => {
  const response = await fetch(`${import.meta.env.VITE_API_URL}/api/hello`)
  const data = await response.json()
  console.log(data.message)
}

console.log("HomeView :: Hello world 👋")
</script>

<template>
  <div class="p-12 w-full max-w-screen-sm mx-auto">
    <h1 class="text-2xl mb-8">Vue.js FastAPI Starter Project Template</h1>
    <p class="mb-4">This is a simple project template for a Vue.js and FastAPI project, set up to be a monorepo.</p>
    <p class="mb-8">This template is intended to be used for prototypes that use generative AI models. Take a look at the README.md file for more information.</p>
    <Button @click="handleSayHello">Say hello to the backend</Button>
  </div>

  <!-- Light / Dark Mode Toggle -->
  <DropdownMenu>
    <DropdownMenuTrigger as-child class="absolute top-4 right-4">
      <Button variant="outline">
        <Icon icon="radix-icons:moon" class="h-[1.2rem] w-[1.2rem] rotate-0 scale-100 transition-all dark:-rotate-90 dark:scale-0" />
        <Icon icon="radix-icons:sun" class="absolute h-[1.2rem] w-[1.2rem] rotate-90 scale-0 transition-all dark:rotate-0 dark:scale-100" />
        <span class="sr-only">Toggle theme</span>
      </Button>
    </DropdownMenuTrigger>
    <DropdownMenuContent align="end">
      <DropdownMenuItem @click="mode = 'light'">
        Light
      </DropdownMenuItem>
      <DropdownMenuItem @click="mode = 'dark'">
        Dark
      </DropdownMenuItem>
      <DropdownMenuItem @click="mode = 'auto'">
        System
      </DropdownMenuItem>
    </DropdownMenuContent>
  </DropdownMenu>
</template>

<style scoped lang="postcss"></style>
