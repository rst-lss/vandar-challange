<template>
  <v-form
    ref="recoveryForm"
    v-model="isValid"
    lazy-validation
    @submit.prevent="submit"
  >
    <!-- mobile input -->
    <base-input
      v-model="phone"
      class="mb-2"
      placeholder="مثال:‌ 09121234567"
      :rules="phoneRules"
      type="tel"
      required
    ></base-input>

    <!-- password input -->
    <base-input
      v-model="password"
      class="mb-2"
      placeholder="رمز عبور جدید"
      :rules="passwordRules"
      type="tel"
      required
    ></base-input>

    <!-- submit button -->
    <v-btn
      type="submit"
      :disabled="!isValid"
      :loading="loading"
      class="mb-2"
      color="#4C9F87"
      large
      block
    >
      ادامه
    </v-btn>

    <div class="text-center pa-4">
      <a href="/login">انصراف</a>
    </div>
  </v-form>
</template>

<script>
import BaseInput from '@/components/base/BaseInput.vue'
export default {
  name: 'PasswordRecoveryForm',
  components: {
    BaseInput,
  },
  data() {
    return {
      phone: '',
      password: '',
      isValid: true,
      loading: false,
      phoneRules: [
        (input) => Boolean(input) || 'این فیلد الزامیست',
        (input) => input.length === 11 || 'شماره تلفن باید 11 رقم باشد',
      ],
      passwordRules: [(input) => Boolean(input) || 'این فیلد الزامیست'],
    }
  },
  methods: {
    recoverPassword() {
      return this.$axios
        .post('/mobile/send', {
          mobile: this.phone,
          password: this.password,
          scope: 'ForgotPass',
        })
        .then(({ data }) => {
          this.$emit('submited', {
            ...data,
            mobile: this.phone,
            password: this.password,
          })
        })
        .catch(({ data }) => {
          this.$emit('error', { message: data.error })
        })
    },

    async submit() {
      await this.$refs.recoveryForm.validate()

      if (this.isValid) {
        this.loading = true
        await this.recoverPassword()
        this.loading = false
      }
    },
  },
}
</script>
