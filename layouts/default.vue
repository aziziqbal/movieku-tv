<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      width="250"
      app
      dark
      color="black"
      class="navigation"
    >
      <v-list-item class="mt-8 mb-4">
        <img
          class="img-logo"
          src="https://www.themoviedb.org/assets/2/v4/logos/v2/blue_short-8e7b30f73a4020692ccca9c88bafe5dcb6f8a62a4c6bc55cd9ba82bb2cd95f6c.svg"
        >
      </v-list-item>
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
          :to="item.to"
          router
          exact
          dense
          class="button-list"
          active-class="highlighted"
          color="black"
        >
          <v-list-item-content>
            <v-list-item-title>{{ item.text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-main style="background: #222b31">
      <v-container style="padding: 20px">
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      drawer: true,
      items: [
        {
          to: '/',
          icon: 'mdi-book-multiple-outline',
          text: 'Top Rated Movie'
        },
        {
          to: '/upcoming',
          icon: 'mdi-folder-image',
          text: 'Upcoming Movie'
        },
        {
          to: '/playing',
          icon: 'mdi-toolbox-outline',
          text: 'Now Playing Movie'
        },
        {
          to: '/popular',
          icon: 'mdi-hospital-building',
          text: 'Popular Movie'
        }
      ]
    }
  },
  methods: {}
}
</script>
<style scoped lang="scss">
.navigation {
  opacity: 1;
  border-right: 0px;
  .img-logo {
    margin-left: auto;
    margin-right: auto;
    margin-bottom: 20px;
    width: 70%;
  }
}
.v-sheet.v-app-bar.v-toolbar:not(.v-sheet--outlined) {
  box-shadow: none;
}
.button-list {
  margin-bottom: 15px;
  height: 40px;
  background-color: transparent;
}
.highlighted {
  background: #222b31;
}
.theme--dark.v-list-item--active:hover::before,
.theme--dark.v-list-item--active::before {
  opacity: 0;
}

@media screen and (max-width: 769px) {
  .search {
    padding-bottom: 0px;
  }
  .projek {
    padding-right: 0px;
    margin-bottom: 10px;
  }
}
</style>
