<template>
  <v-app>
    <v-container fluid>
      <v-radio-group mandatory v-model="row" row>
        <template v-slot:label>
          <div>Your favorite <strong>transportation</strong></div>
        </template>
        <v-radio label="徒歩" value="walk"></v-radio>
        <v-radio label="チャリ" value="bike"></v-radio>
        <v-radio label="車" value="car"></v-radio>
      </v-radio-group>
      <v-radio-group mandatory v-model="row" row>
        <template v-slot:label>
          <div>Your favorite <strong>genre of food</strong></div>
        </template>
        <v-radio label="ラーメン" value="ramen"></v-radio>
        <v-radio label="カレー" value="curry"></v-radio>
        <v-radio label="その他" value="other"></v-radio>
      </v-radio-group>
      <v-btn
      class="mx-2"
      fab
      dark
      color="indigo"
    >
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
}
</script>
