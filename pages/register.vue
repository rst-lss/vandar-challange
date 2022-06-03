<template>
  <div class="register-page">
    <div class="text-center">
      <h1 class="pa-2">چند کلیک تا ساخت حساب</h1>
      <div>تکمیل تمامی بخش ها الزامیست</div>

      <v-form
        ref="registerForm"
        v-model="isValid"
        class="pt-4"
        lazy-validation
        @submit.prevent="submit"
      >
        <!-- mobile input -->
        <base-input
          v-model="register.nationalNumber"
          class="mb-2"
          placeholder="کد ملی"
          :rules="rules.nationalNumber"
          type="number"
          required
        ></base-input>

        <!-- first name input -->
        <base-input
          v-model="register.fname"
          class="mb-2"
          placeholder="نام"
          :rules="rules.fname"
          type="text"
          required
        ></base-input>

        <!-- last name input -->
        <base-input
          v-model="register.lname"
          class="mb-2"
          placeholder="نام خانوادگی"
          :rules="rules.lname"
          type="text"
          required
        ></base-input>

        <!-- date picker -->
        <base-date-picker @submit="register.date = $event"></base-date-picker>

        <!-- password input -->
        <base-input
          v-model="register.password"
          :type="showPass ? 'text' : 'password'"
          placeholder="رمز عبور"
          class="mb-2"
          :rules="rules.password"
          :append-icon="showPass ? 'mdi-eye' : 'mdi-eye-off'"
          @focus="errorMessage = null"
          @click:append="showPass = !showPass"
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
      </v-form>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.register-page {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>
