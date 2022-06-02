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
}
</script>

<style lang="scss" scoped></style>
