<script setup lang="ts">
import { Popover, PopoverButton, PopoverPanel } from '@headlessui/vue';
import { LogOutIcon, StarIcon, UserRoundIcon } from 'lucide-vue-next';

defineProps({
  minecraftUuid: String,
});

const handleLogout = async () => {
  document.cookie = "token=; expires=Thu, 01 Jan 1970 00:00:00 GMT; path=/"
};
</script>

<template>
  <div>
    <Popover class="relative">
      <PopoverButton class="flex gap-2 items-center">
        <img class="border rounded-full size-8" :src="`https://mc-heads.net/avatar/${minecraftUuid}/100`"/>
      </PopoverButton>
      <transition
          enter-active-class="transition duration-200 ease-out"
          enter-from-class="translate-y-1 opacity-0"
          enter-to-class="translate-y-0 opacity-100"
          leave-active-class="transition duration-150 ease-in"
          leave-from-class="translate-y-0 opacity-100"
          leave-to-class="translate-y-1 opacity-0"
      >
        <PopoverPanel
            class="absolute bg-white border-1 border-gray-400 max-w-sm mt-4 px-2 py-4 right-0 rounded-xl shadow-lg transform w-64 z-10">
          <div class="flex items-center mb-4">
            <p class="font-semibold text-gray-800 text-xl">@tksimeji</p>
            <div class="flex items-center ml-auto px-2 py-1 rounded-2xl">
              10
              <StarIcon color="#d2a04a" fill="#d2a04a" :size="14"/>
            </div>
          </div>

          <div class="bg-gray-200 border-1 border-gray-400/60 flex flex-col overflow-hidden rounded-2xl text-sm">
            <a
                class="cursor-pointer flex gap-4 items-center p-3 hover:bg-gray-300"
                :href="`/players/${minecraftUuid}`"
            >
              <UserRoundIcon :size="16"/>
              プロフィール
            </a>
            <button
                class="cursor-pointer flex font-semibold gap-4 items-center p-3 text-red-500 hover:bg-gray-300"
                @click="handleLogout"
            >
              <LogOutIcon :size="16"/>
              ログアウト
            </button>
          </div>
        </PopoverPanel>
      </transition>
    </Popover>
  </div>
</template>

<style scoped>

</style>