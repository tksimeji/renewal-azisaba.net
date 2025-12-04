<script setup>
import { computed } from 'vue'

const props = defineProps({
  placeholder: { type: String, required: true },
  modelValue: { type: String, default: '' } // ← これを追加
})

const emit = defineEmits(['update:modelValue'])

const model = computed({
  get: () => props.modelValue,
  set: (value) => emit('update:modelValue', value),
})

const uniqueId = `fi-${Math.random().toString(36).substring(2, 8)}`
</script>

<template>
  <div class="relative w-full max-w-sm">
    <input
        :id="uniqueId"
        type="text"
        class="peer block w-full rounded-lg border border-gray-700 px-2 py-4 pt-5 pb-2
             placeholder-transparent focus:border-azisaba-soft-tail focus:ring-2 focus:ring-azisaba-soft-tail focus:outline-none"
        placeholder=" "
        v-model="model"
    />
    <label
        :for="uniqueId"
        class="absolute left-3 top-1/2 -translate-y-1/2 px-1 text-gray-500 transition-all
             peer-placeholder-shown:text-base
             peer-focus:text-xs peer-focus:top-4 peer-focus:text-azisaba-soft-tail
             peer-[:not(:placeholder-shown)]:text-xs peer-[:not(:placeholder-shown)]:top-4 peer-[:not(:placeholder-shown)]:text-azisaba-soft-tail"
    >
      {{ placeholder }}
    </label>
  </div>
</template>