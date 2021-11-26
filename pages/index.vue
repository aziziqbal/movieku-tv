<template>
  <v-container>
    <v-row align="center">
      <v-col cols="12" md="6" align="start">
        <div class="title-card">
          Top Rated Movie
        </div>
      </v-col>
      <v-col cols="12" md="4" class="ml-auto">
        <v-text-field
          v-model="search"
          solo
          dense
          hide-details
          label="Search movie"
          prepend-inner-icon="mdi-magnify"
        />
      </v-col>
    </v-row>
    <div class="title-card" />
    <v-row align="center" class="mt-10">
      <v-col
        v-for="(item, index) in filteredList"
        :key="index"
        cols="6"
        md="4"
        align="start"
      >
        <div class="card-movie">
          <img
            :src="'https://image.tmdb.org/t/p/w500' + item.backdrop_path"
            class="img-tmb"
          >

          <v-progress-circular
            :rotate="360"
            :size="40"
            :width="4"
            :value="item.vote_average"
            color="white"
            class="rating"
          >
            {{ item.vote_average }}%
          </v-progress-circular>
          <v-row class="mt-2">
            <v-col cols="10">
              <div class="title-movie">
                {{ item.title }}
              </div>

              <div class="release-date">
                {{ item.release_date }}
              </div>
            </v-col>
            <v-col cols="2">
              <v-btn class="btn-watchlist" x-small fab dark color="indigo">
                <v-icon dark>
                  mdi-plus
                </v-icon>
              </v-btn>
            </v-col>
          </v-row>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  data () {
    return {
      isLoading: false,
      data: [],
      show: false,
      genre: {},
      search: ''
    }
  },
  computed: {
    filteredList () {
      return this.data.filter((items) => {
        return items.title.toLowerCase().includes(this.search.toLowerCase())
      })
    }
  },
  mounted () {
    this.getGenre()
  },
  methods: {
    async getGenre () {
      this.isLoading = true
      await this.$axios
        .$get(
          'https://api.themoviedb.org/3/genre/movie/list?api_key=397d703720f8ff83a7b03b232645e39e&language=en-US'
        )
        .then((res) => {
          this.isLoading = false
          this.genre = res.genres
          this.getData()
        })
        .catch((err) => {
          this.isLoading = false
          console.log('error : ', err)
        })
    },
    async getData () {
      this.isLoading = true
      await this.$axios
        .$get(
          this.$axios.defaults.baseURL +
            '/top_rated?api_key=397d703720f8ff83a7b03b232645e39e&language=en-US&page=1'
        )
        .then((res) => {
          this.isLoading = false
          this.data = res.results
        })
        .catch((err) => {
          this.isLoading = false
          console.log('error : ', err)
        })
    }
  }
}
</script>
<style lang="scss" scoped>
.title-card {
  font-size: 20px;
  color: white;
}
.card-movie {
  height: 100%;
  width: 100%;
  position: relative;
  cursor: pointer;
  .movies {
    padding: 0px;
  }
  .img-tmb {
    width: 100%;
    border-radius: 10px;
    height: 200px;
    object-fit: cover;
  }
  .rating {
    position: absolute;
    top: 180px;
    left: 10px;
    background-color: black;
    border-radius: 50%;
    color: white;
    font-size: 10px;
  }
  .title-movie {
    font-size: 14px;
    color: white;
    font-weight: bold;
  }
  .release-date {
    font-size: 13px;
    margin-top: 2px;
    color: white;
  }
}
</style>
