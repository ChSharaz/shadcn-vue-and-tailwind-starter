<script setup>
import { useVModel } from '@vueuse/core'
import { computed, ref } from 'vue'
import { Input } from '@/components/ui/input'

const props = defineProps({
  name: {
    type: String
  },
  label: {
    type: String
  },
  modelValue: {
    type: [String, Number]
  },
  error: {
    type: String,
    default: ''
  },
  validate: {
    type: Function
  },
  class: {
    type: [String, Object, Array],
    default: ''
  }
})

const emits = defineEmits(['update:modelValue'])
const modelValue = useVModel(props, 'modelValue', emits, {
  passive: true,
  defaultValue: props.defaultValue
})

const handleBlur = () => {
  props.validate(props.name)
}

const inputClass = computed(() => {
  return {
    'border-red-500': props.error,
    ...props.class
  }
})
</script>

<template>
  <div>
    <label :for="name" class="block text-sm font-medium text-gray-700 mb-1">{{ label }}</label>
    <Input v-bind="$attrs" :id="name" v-model="modelValue" :class="inputClass" @blur="handleBlur" />
    <span v-if="error" class="text-red-500 text-sm mt-1">{{ error }}</span>
  </div>
</template>
