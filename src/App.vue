<template>
    <v-app class="bg">
      <v-main>
        <router-view/>
      </v-main>
    </v-app>
</template>

<style scoped>
.bg {
  background-image: url("assets/bg.png");
  background-repeat: no-repeat;
  background-size: cover;
}
</style>
