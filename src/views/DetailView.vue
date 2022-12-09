<template>
  <v-row class="my-6" align="center" justify="center">
    <v-col cols="4">
<!--   $route.params.zipcode   -->
      <SearchForm></SearchForm>
    </v-col>
  </v-row>
  <v-row class="" align="center" justify="center">
    <v-col cols="6">
      <v-card>
        <v-card-item v-if="status=='done'">
          <h2 class="text-center my-4">
            <span style="color: red;">〒</span>{{ $route.params.zipcode }}
            {{ address }}
          </h2>
          <iframe
              v-bind:src="googleMapUrl"
              width="100%"
              height="500"
              frameborder="0"
              style="border:0;"
              allowfullscreen=""
          ></iframe>
        </v-card-item>
        <v-card-item align="center" justify="center" style="height: 350px;" v-if="status=='loading'">
          <hour-glass></hour-glass>
          <small>検索中</small>
        </v-card-item>
        <v-card-item align="center" justify="center" style="height: 350px;" v-if="status=='error'">
          <v-icon>mdi-help-circle-outline</v-icon> <small>見つかりませんでした</small>
        </v-card-item>
      </v-card>
    </v-col>
  </v-row>
  <div align="center" justify="center">
    <v-btn
        class="mt-10"
        fab
        dark
        large
        color="blue"
        to="/"
    >
      <v-icon dark>
        mdi-arrow-left
      </v-icon>
      ホームへ
    </v-btn>
  </div>
</template>


<script>
import axios from 'axios';
import {HourGlass} from 'vue-loading-spinner'
import SearchForm from "@/components/SearchForm";

export default {
  name: "DetailView",
  components: {
    SearchForm,
    HourGlass,
  },
  data() {
    return {
      status: 'loading',
      address: '',
      googleMapUrl: '',
      mdiHelpCircleOutline: '',
    }
  },
  watch: {
    $route () {
      location.reload()
    }
  },
  mounted() {
    let apiUrl = 'https://zipcloud.ibsnet.co.jp/api/search?zipcode=';
    axios.get(apiUrl + this.$route.params.zipcode)
        .then((response) => {
          // handle success(axiosの処理が成功した場合に処理させたいことを記述)
          console.log(response);
          let address = response.data.results[0];
          console.log(address)
          console.log(this.address)
          this.address = address.address1 + address.address2 + address.address3;
          this.googleMapUrl = 'https://maps.google.com/maps?output=embed&t=h&hl=ja&z=18&q=' + this.address;
          this.status = 'done';
        })
        .catch((error) => {
          // handle error(axiosの処理にエラーが発生した場合に処理させたいことを記述)
          console.log(error);
          this.status = 'error';
        })
        .finally(function () {
          // always executed(axiosの処理結果によらずいつも実行させたい処理を記述)
        });
  },
  methods: {
    sleep(waitMsec) {
      var startMsec = new Date();

      // 指定ミリ秒間だけループさせる（CPUは常にビジー状態）
      while (new Date() - startMsec < waitMsec);
    }
  }
}
</script>

<style scoped>

</style>