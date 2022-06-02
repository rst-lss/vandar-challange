<template>
  <v-form
    ref="passwordForm"
    v-model="isValid"
    lazy-validation
    @submit.prevent="submitPassword"
  >
    <!-- password input -->
    <base-input
      v-model="password"
      :type="showPass ? 'text' : 'password'"
      placeholder="رمز عبور"
      class="mb-2"
      :rules="rules"
      :error-messages="errorMessage"
      :append-icon="showPass ? 'mdi-eye' : 'mdi-eye-off'"
      @focus="errorMessage = null"
      @click:append="showPass = !showPass"
    ></base-input>

    <!-- remember me checkbox -->
    <div class="remember-me">
      <v-checkbox
        v-model="rememberMe"
        class="mt-0 white--text"
        color="gray"
        label="مرا به خاطر بسپار"
        hide-details
      ></v-checkbox>
    </div>

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

    <div class="d-flex justify-space-around pa-4">
      <a href="/forgot-password">بازیابی رمزعبور</a>
      <v-divider vertical inset></v-divider>
      <a href="/login">تغییر شماره</a>
    </div>
  </v-form>
</template>

<script>
import BaseInput from '@/components/base/BaseInput.vue'
export default {
  name: 'PasswordForm',
  components: {
    BaseInput,
  },
  props: {
    phone: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      password: '',
      rememberMe: false,
      isValid: true,
      loading: false,
      errorMessage: null,
      rules: [(input) => Boolean(input) || 'این فیلد الزامیست'],
      showPass: false,
    }
  },
  methods: {
    login() {
      return this.$auth
        .login({
          mobile: this.phone,
          password: this.password,
        })
        .then(({ data }) =>
          this.$emit('submited', {
            ...data,
            login: { password: this.password, mobile: this.phone },
          })
        )
        .catch(({ data }) => {
          this.$emit('error', data)
        })
    },

    async submitPassword() {
      await this.$refs.passwordForm.validate()

      if (this.isValid) {
        this.loading = true
        await this.login()
        this.loading = false
      }
    },
  },
}
</script>

<style lang="scss" scoped>
.remember-me {
  padding: 0.5rem;
  background-color: #e5e5e5;
  border-radius: 5px;
  margin-bottom: 1rem;
  direction: rtl;
}
</style>
