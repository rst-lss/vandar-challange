<template>
  <v-app>
    <v-app-bar dark flat dense app>
      <v-spacer></v-spacer>
      <img
        id="app-bar-logo"
        src="@/assets/images/vandar-small-logo.svg"
        alt="vandar small logo"
        style="width: 50px; height: 50px"
      />
      <v-spacer></v-spacer>
    </v-app-bar>
    <v-main>
      <v-container class="content-wrapper" fluid>
        <div id="bg-circle"></div>
        <Nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<style scoped lang="scss">
.content-wrapper {
  padding: 0;
  height: 100%;
  position: relative;
  overflow: hidden;

  #bg-circle {
    position: absolute;
    bottom: -100%;
    left: 50%;
    width: 400vh;
    height: 300vh;

    background-color: #cfcfcf;
    border-radius: 50%;
    opacity: 0.1;
  }
}

#app-bar-logo {
  position: relative;
  bottom: -1.2rem;
}
</style>
