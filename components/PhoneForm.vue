<template>
  <v-form
    ref="phoneForm"
    v-model="isValid"
    lazy-validation
  >
    <!-- mobile input -->
    <base-input
      v-model="phone"
      class="mb-2"
      placeholder="مثال:‌ 09121234567"
      :error-messages="errorMessage"
      :rules="rules"
      type="tel"
      required
      @focus="errorMessage = null"
    ></base-input>

    <!-- submit button -->
    <v-btn
      type="submit"
      :disabled="!isValid"
      :loading="loading"
      color="#4C9F87"
      large
      block
    >
      ادامه
    </v-btn>
  </v-form>
</template>

<script>
import BaseInput from '@/components/base/BaseInput.vue'
export default {
  name: 'PhoneForm',
  components: {
    BaseInput,
  },
  data() {
    return {
      phone: '',
      isValid: true,
      loading: false,
      errorMessage: null,
      rules: [
        (input) => Boolean(input) || 'این فیلد الزامیست',
        (input) => input.length === 11 || 'شماره تلفن باید 11 رقم باشد',
      ],
    }
  },
  methods: {
}
</script>
