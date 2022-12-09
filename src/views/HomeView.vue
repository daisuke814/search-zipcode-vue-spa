<template>
  <v-row style="height: 100%;" align="center" justify="center">
    <v-col cols="4">
      <h1 class="mb-2 text-center text-white"><span style="color: red;">〒</span> 郵便番号から住所を検索</h1>
      <SearchForm></SearchForm>
    </v-col>
  </v-row>
</template>

<script>

import SearchForm from "@/components/SearchForm";

export default {
  name: "HomeView",
  components: {
    SearchForm
  },
}
</script>