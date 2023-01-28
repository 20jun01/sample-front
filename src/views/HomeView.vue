<template>
  <v-app id ="unscrollable">
    <div v-if="loading">
      <v-progress-linear indeterminate color="teal"></v-progress-linear>
    </div>
    <v-container fluid>
      <v-radio-group mandatory v-model="row" row>
        <template v-slot:label>
          <div>Your favorite <strong>transportation</strong></div>
        </template>
        <v-radio label="徒歩" value="walk"></v-radio>
        <v-radio label="チャリ" value="bike"></v-radio>
        <v-radio label="車" value="car"></v-radio>
      </v-radio-group>
      <v-radio-group mandatory v-model="row2" row>
        <template v-slot:label>
          <div>Your favorite <strong>genre of food</strong></div>
        </template>
        <v-radio label="ラーメン" value="ラーメン"></v-radio>
        <v-radio label="カレー" value="カレー"></v-radio>
        <v-radio label="その他" value=""></v-radio>
      </v-radio-group>
      <v-btn class="mx-2" fab dark color="indigo" @click="search">
        <v-icon dark>
          mdi-arrow-top-left-thick
        </v-icon>
      </v-btn>
    </v-container>
  </v-app>
</template>

<script>
export default {
  name: 'HomeView',
  data() {
    return {
      keywords: [],
      latitude: 0,
      longitude: 0,
      row: null,
      row2: null,
      loading: false,
    }
  },
  methods: {
    search() {
      this.loading = true
      if (!navigator.geolocation) {
        alert('現在地情報を取得できませんでした。お使いのブラウザでは現在地情報を利用できない可能性があります。エリアを入力してください。')
        return
      }

      const options = {
        enableHighAccuracy: false,
        timeout: 5000,
        maximumAge: 0
      }

      navigator.geolocation.getCurrentPosition(this.success, this.error, options)
    },

    success(position) {
      this.latitude = position.coords.latitude
      this.longitude = position.coords.longitude
      this.$axios
        .post(process.env.VUE_APP_SERVER_URL + "/map", {
          location: this.latitude + "," + this.longitude,
          keywords: [this.row2],
          radius: this.cast_to_meters(this.row),
        })
        .then((response) => (this.$router.push({ name: 'result', params: { src: "https://www.google.com/maps/embed/v1/place?key=" + process.env.VUE_APP_GOOGLE_MAPS_API_KEY + "&q=" + response.data.name, url: response.data.url, name: response.data.name } }),
          this.loading = false
        ))
        .catch((error) => console.log(error));
    },

    error(error) {
      switch (error.code) {
        case 1: //PERMISSION_DENIED
          alert('位置情報の利用が許可されていません')
          break
        case 2: //POSITION_UNAVAILABLE
          alert('現在位置が取得できませんでした')
          break
        case 3: //TIMEOUT
          alert('タイムアウトになりました')
          break
        default:
          alert('現在位置が取得できませんでした')
          break
      }
    },

    cast_to_meters(row) {
      switch (row) {
        case "walk":
          return 500
        case "bike":
          return 1000
        case "car":
          return 2000
        default:
          return 500
      }
    }
  }
}
</script>
