<template>
  <v-form
    ref="otpForm"
    v-model="isValid"
    lazy-validation
    @submit.prevent="submitOtp"
  >
    <v-otp-input v-model="key" length="5" @finish="submitOtp"></v-otp-input>
    <v-btn type="submit" :disabled="!isValid" color="#4C9F87" large block>
      ورود
    </v-btn>
  </v-form>
</template>

<script>
export default {
  name: 'OtpForm',
  props: {
    phone: { type: String, required: true },
  },
  data() {
    return {
      key: '',
      isValid: false,
      rules: [(input) => Boolean(input) || 'این فیلد الزامیست'],
    }
  },
  methods: {
    // checks code and emit submited event
    verifyOtp() {
      return this.$axios
        .post('/mobile/verify', {
          mobile: this.phone,
          key: this.key,
          scope: 'Register',
        })
        .then(() => {
          // notify parent component about success
          this.$emit('submited', { mobile: this.phone })
        })
        .catch(({ response: { data } }) => {
          // notify parent component about error
          this.$emit('error', { message: data.error })
        })
    },
    async submitOtp() {
      await this.$refs.otpForm.validate()

      if (this.isValid) {
        this.loading = true
        await this.verifyOtp()
        this.loading = false
      }
    },
  },
}
</script>

<style lang="scss" scoped></style>
