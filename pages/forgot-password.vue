<template>
  <div class="forgot-pass-form">
    <v-slide-y-transition>
      <div v-show="errorMessage !== null" class="alert-box">
        {{ errorMessage }}
      </div>
    </v-slide-y-transition>

    <v-spacer></v-spacer>

    <div class="mb-8">
      <h2 class="font-wegiht-bold mb-2">{{ title }}</h2>
      <div class="text-subtitle">{{ subtitle }}</div>
    </div>

    <!-- dynamic component -->
    <component
      :is="currentView.name"
      v-bind="currentView.props"
      v-on="currentViewEventHandlers"
    ></component>

    <v-spacer></v-spacer>
  </div>
</template>

<script>
import PasswordRecoveryForm from '@/components/PasswordRecoveryForm.vue'
import OtpForm from '@/components/OtpForm.vue'

export default {
  components: {
    PasswordRecoveryForm,
    OtpForm,
  },
  layout: 'login',
  data() {
    return {
      title: 'بازیابی رمز عبور',
      subtitle: 'ابتدا رمز جدید را انتخاب کنید',
      errorMessage: null,
      currentView: { name: 'PasswordRecoveryForm', props: {} },
    }
  },
  computed: {
    // handling events on dynamic component
    currentViewEventHandlers() {
      return this.currentView.name === 'PasswordRecoveryForm'
        ? {
            submited: this.codeIsSent,
            error: this.handleError,
          }
        : {
            submited: this.otpVerified,
            error: this.handleError,
          }
    },
  },
  methods: {
    codeIsSent({ mobile }) {
      this.subtitle = 'کد ارسال شده به شماره ' + mobile + ' را وارد کنید'
      this.currentView = {
        name: 'OtpForm',
        props: {
          phone: mobile,
          scope: 'ForgotPass',
        },
      }
    },

    otpVerified() {
      this.$router.push({ path: '/login' })
    },

    handleError({ message }) {
      this.errorMessage = message
      setTimeout(() => {
        this.errorMessage = null
      }, 3000)
    },
  },
}
</script>

<style lang="scss" scoped>
.forgot-pass-form {
  flex: 1 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;

  text-align: center;
  padding: 2rem 7.5rem 0;
}

.alert-box {
  padding: 0.875rem 1rem;
  border-radius: 0.25rem;

  background: #d44d42;
  color: white;
  border-radius: 4px;
  transition: opacity 0.3s ease;
}
</style>
