<template>
  <v-card dark height="50px" class="headers">
    <v-container>
      <v-toolbar color="black">
        <img
          src="https://skempin.github.io/reactjs-tmdb-app/images/tmdb.svg"
          class="img-logo"
          style="height: 40px"
        >

        <v-spacer />
        <v-btn text>
          Top Rated
        </v-btn>
        <v-btn text>
          Upcoming
        </v-btn>
        <v-btn text>
          Populer
        </v-btn>
      </v-toolbar>
    </v-container>
  </v-card>
</template>
<style lang="scss" scoped>
.headers {
  background-color: black;
  .img-logo {
    height: 40px;
    cursor: pointer;
  }
}
</style>
