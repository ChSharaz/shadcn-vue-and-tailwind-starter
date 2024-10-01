<template>
  <form @submit.prevent="handleSubmit">
    <slot :v="v" :errors="errors" :validate="validate"></slot>
  </form>
</template>

<script>
import { useVuelidate } from '@vuelidate/core'
import { reactive, computed } from 'vue'

export default {
  name: 'FormWrapper',
  props: {
    initialValues: {
      type: Object,
      required: true
    },
    validations: {
      type: Object,
      required: true
    },
    onSubmit: {
      type: Function,
      required: true
    }
  },
  setup(props) {
    const state = reactive(props.initialValues)
    const v = useVuelidate(props.validations, state, { $lazy: true })

    const errors = computed(() => {
      const errors = {}
      Object.keys(v.value).forEach((key) => {
        if (v.value[key]?.$error) {
          errors[key] = v.value[key].$errors[0].$message
        }
      })
      return errors
    })

    const validate = async (fieldName) => {
      await v.value[fieldName].$touch()
    }

    const handleSubmit = async () => {
      const isValid = await v.value.$validate()
      if (isValid) {
        props.onSubmit(state)
      }
    }

    return { v, errors, handleSubmit, validate }
  }
}
</script>
