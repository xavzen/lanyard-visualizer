<script lang="ts" setup>
import { onStartTyping, useTitle } from "@vueuse/core"
import { ref } from "vue"
import { useRouter } from "vue-router"

// Iconsicon-tabler-brand-discord
import IconBrandDiscord  from "~icons/tabler/brand-discord"
import IconGithub from "~icons/tabler/brand-github"
import IconLink from "~icons/tabler/link"

const router = useRouter()

const userId = ref("")
const inputFocused = ref(false)
const inputElement = ref<HTMLInputElement | null>(null)

const handleSubmit = async () => {
  if (!userId.value) return
  router.push(`/${userId.value}`)
}

// Hooks
useTitle("Lanyard Visualizer")

onStartTyping(() => {
  inputElement?.value?.focus()
})
</script>

<template>
  <div>
    <header class="h-screen relative grid place-items-center p-8 md:p-16">
      <div
        v-motion-fade
        class="absolute -z-1 overflow-hidden pointer-events-none inset-0 grid place-items-center"
      >
        <img
          src="/header-background.png"
          alt="Stylistic header background"
          class="object-cover h-full w-full max-w-screen max-h-screen opacity-2"
        />
      </div>

      <div v-motion-fade :delay="300" class="flex flex-col items-center gap-6">
        <img src="/Logo.png" alt="Lanyard logo" class="h-12" />

   

        <p class="text-white/50 md:text-lg md:w-9/10 text-center font-medium">
          Neat little user presence visualizer
        </p>
        <div class="relative w-full md:w-full flex justify-center">
          <input
            v-model="userId"
            ref="inputElement"
            class="appearance-none pl-3 pr-20 placeholder-white/20 w-full bg-transparent outline-none py-2 border-[1.5px] border-white/10 hover:border-white/20 focus:border-white/30 transition-all rounded-lg"
            placeholder="Enter your Discord user ID"
            @focus="inputFocused = true"
            @blur="inputFocused = false"
            @keydown.enter="handleSubmit"
          />

          <div class="absolute inset-y-0 right-0 pr-4 flex items-center">
            <button
              type="button"
              class="text-white/20 font-medium select-none hover:text-white/40 transition-colors text-xs uppercase"
              :class="userId.length >= 18 && 'text-white/40'"
              @click="handleSubmit"
            >
              Submit
            </button>
          </div>
          
        </div>
        <iframe src="https://discord.com/widget?id=1031602387300909056&theme=dark" width="350" height="400" allowtransparency="true" frameborder="0" sandbox="allow-popups allow-popups-to-escape-sandbox allow-same-origin allow-scripts"></iframe>    

       


      </div>
</header>
  </div>
</template>

<style lang="scss">
input[type="number"] {
  -moz-appearance: textfield;
  appearance: textfield;

  &::-webkit-outer-spin-button,
  &::-webkit-inner-spin-button {
    -webkit-appearance: none;
    margin: 0;
  }
}
</style>