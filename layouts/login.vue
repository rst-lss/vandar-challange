<template>
  <v-app>
    <v-main>
      <v-container class="pa-0" fluid style="height: 100%">
        <div class="login-layout">
          <div class="ad-container">
            <div class="ad-image">
              <img src="~assets/images/image-holder.svg" alt="image holder" />
            </div>
            <div class="text-center pa-5">
              <div class="text-body-1 font-weight-bold mb-1">
                تسویه به هرشخصی در هر بانکی که بخواهید
              </div>
              <div class="mb-8 text-body-2 font-weight-light">
                تسویه پول‌های دریافتی به بیشمار حساب
              </div>
              <a>بیشتر بخوانید</a>
            </div>
          </div>
          <div class="right-container">
            <Nuxt />
            <div class="logo-container">
              <img src="~/assets/images/vandar-logo.svg" alt="vandar logo" />
            </div>
          </div>
        </div>
      </v-container>
    </v-main>
  </v-app>
</template>

<style lang="scss" scoped>
.login-layout {
  display: flex;
  height: 100%;
}

.ad-image {
  text-align: center;
  border: 1px solid #e6e6e6;
}

.ad-container {
  flex: 1 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 2rem;

  @media screen and (max-width: 1000px) {
    display: none;
  }
}

.right-container {
  flex: 1 0 auto;
  background-color: #f5f5f5;
  max-width: 535px;
  display: flex;
  flex-direction: column;
  justify-content: center;

  @media screen and (max-width: 1000px) {
    max-width: 100%;
  }
}

.logo-container {
  text-align: center;
  padding: 1.5rem;
}
</style>
