<template>
  <FormWrapper :initial-values="initialValues" :validations="validations" :on-submit="onSubmit">
    <template v-slot="{ errors, validate }">
      <CInput
        name="email"
        label="Email"
        v-model="initialValues.email"
        :error="errors.email"
        :validate="validate"
      />
      <div class="mt-3">
        <CInput
          name="password"
          label="Password"
          type="password"
          v-model="initialValues.password"
          :error="errors.password"
          :validate="validate"
        />
      </div>
      <Button type="submit" variant="primary" class="w-full mt-6"> Sign In </Button>
    </template>
  </FormWrapper>
</template>

<script>
import { reactive } from 'vue'
import { required, email } from '@vuelidate/validators'
import FormWrapper from './FormWrapper.vue'
import { Button } from '@/components/ui/button'

export default {
  name: 'ExampleForm',
  components: {
    FormWrapper,
    Button
  },
  setup() {
    const initialValues = reactive({
      email: '',
      password: ''
    })

    const validations = {
      email: { required, email },
      password: { required }
    }

    const onSubmit = (values) => {
      console.log('Form submitted with:', values)
    }

    return {
      initialValues,
      validations,
      onSubmit
    }
  }
}
</script>
