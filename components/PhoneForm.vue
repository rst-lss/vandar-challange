<template>
  <v-form
    ref="phoneForm"
    v-model="isValid"
    lazy-validation
    @submit.prevent="submitPhone"
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
    // checks if user has registered or not
    checkMobile() {
      return this.$axios
        .post('register/check/mobile', { mobile: this.phone })
        .then(({ data }) => {
          // notify parent component
          this.$emit('submited', data)
        })
        .catch(({ data }) => {
          // show error tooltip for phone input
          this.errorMessage = data.message

          // emit event to notify parent component
          this.$emit('error', data)
        })
    },

    async submitPhone() {
      this.$refs.phoneForm.validate()

      if (this.isValid) {
        this.loading = true
        await this.checkMobile()
        this.loading = false
      }
    },
  },
}
</script>
