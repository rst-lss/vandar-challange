<template>
  <div class="login-form">
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
import PhoneForm from '@/components/PhoneForm.vue'
import PasswordForm from '@/components/PasswordForm.vue'
import OtpForm from '@/components/OtpForm.vue'

export default {
  components: {
    PhoneForm,
    PasswordForm,
    OtpForm,
  },
  layout: 'login',
  data() {
    return {
      title: 'ورود به دنیای امن پرداخت',
      subtitle: 'ابتدا تلفن همراه خود را وارد کنید',
      errorMessage: null,
      currentView: { name: 'PhoneForm', props: {} },
    }
  },
  computed: {
    // handling events on dynamic component
    currentViewEventHandlers() {
      switch (this.currentView.name) {
        case 'PhoneForm':
          return {
            submited: this.mobileChecked,
            error: this.handleError,
          }
        case 'PasswordForm':
          return {
            submited: this.loggedIn,
            error: this.handleError,
          }
        case 'OtpForm':
          return {
            submited: this.otpVerified,
            error: this.handleError,
          }
        default:
          return {}
      }
    },
  },
  methods: {
    mobileChecked({ mobile, message, status }) {
      if (status === -1) {
        this.handleError({ message })
        return
      }
      if (message === 'Registered') {
        this.subtitle = 'رمز عبور حساب با شماره ' + mobile + ' را وارد کنید'

        // show password form (user has registered before)
        this.currentView = {
          name: 'PasswordForm',
          props: {
            phone: mobile,
          },
        }
      } else if (message === 'SMS Send') {
        this.subtitle = 'کد ارسال شده به شماره ' + mobile + ' را وارد کنید'
        // show otp form (user has not registered before)
        this.currentView = {
          name: 'OtpForm',
          props: {
            phone: mobile,
          },
        }
      }
    },

    logedIn({ mobile, password, message }) {
      this.$router.push({ name: 'index' })
    },

    otpVerified({ mobile }) {
      this.$router.push({ path: '/register', props: { phone: mobile } })
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
.login-form {
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
