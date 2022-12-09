<template>
  <v-text-field
      density="compact"
      variant="solo"
      label="郵便番号を検索"
      prepend-inner-icon="mdi-magnify"
      v-model="zipcode"
      @keydown.enter="submitZipcode"
      placeholder="郵便番号を入力してください"
      single-line
      hide-details
  ></v-text-field>
</template>

<script>

import Router from "@/router";

export default {
  name: 'SearchForm',
  data() {
    return {
    }
  },
  methods: {
    submitZipcode() {
      Router.push({
        name: 'detail',
        params: {
          zipcode: this.zipcode
        }
      });
    }
  },
  mounted() {
    this.zipcode = this.$route.params.zipcode;
  }
}
</script>
