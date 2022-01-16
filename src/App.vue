<template>
    <SideBar :totalWishList="wishList.length" />
    <Home
      :onAddWishListItem="addWishListHandler"
      :onRemoveWishListItem="removeWishListItemHandler"
      :wishListItem="wishList"
      :items="dataAPI"
      :popularItems="popularItems"
      :mainData="mainData"
      :onSearch="getSearchedTitle"
      :loadingSearch="loadingSearch"
      :loadingPage="loadingPage"
      :errored="errored"
      :mainPosters="mainPosters"
      :mainBackDrops="mainBackDrops"
      :mainPlot="mainPlot"
    />
</template>

<script>
import SideBar from './components/SideBar.vue'
import Home from './components/Home.vue'
const axios = require("axios");

export default {
  name: 'App',
  components: {
    SideBar,
    Home,
  },
  data() {
    return {
      dummyItems:  [
          {"id":"tt4566758","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BNDliY2E1MjUtNzZkOS00MzJlLTgyOGEtZDg4MTI1NzZkMTBhXkEyXkFqcGdeQXVyNjMwMzc3MjE@._V1_Ratio0.7273_AL_.jpg","title":"Mulan","description":"(2020)"},
          {"id":"tt0120762","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BODkxNGQ1NWYtNzg0Ny00Yjg3LThmZTItMjE2YjhmZTQ0ODY5XkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_Ratio0.7273_AL_.jpg","title":"Mulan","description":"(1998)"},
          {"id":"tt1308138","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BNmMyMTY2YmEtZjM2ZS00ZWQ5LWE4YjEtOGMxOGZhY2RlZjJjXkEyXkFqcGdeQXVyNDM2OTEyOTM@._V1_Ratio0.7273_AL_.jpg","title":"Mulan: Rise of a Warriorrrrrrr","description":"(2009)"},
          {"id":"tt0279967","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BODEzMmIxOGMtY2RhYS00YTFiLThkZmYtMDlmZGJlYzg0NWEzXkEyXkFqcGdeQXVyNjk1Njg5NTA@._V1_Ratio0.7273_AL_.jpg","title":"Mulan II","description":"(2004) (Video)"},
          {"id":"tt2753110","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BNTA0YWQ3OTgtNjNiNC00YmU5LWI5NmEtMGUxOTY0ODgyNzM4XkEyXkFqcGdeQXVyMzU3MTc5OTE@._V1_Ratio0.7273_AL_.jpg","title":"Mulaney","description":"(2014) (TV Series)"}
      ],
      mainPosters: [
        "https://imdb-api.com/images/original/MV5BNDliY2E1MjUtNzZkOS00MzJlLTgyOGEtZDg4MTI1NzZkMTBhXkEyXkFqcGdeQXVyNjMwMzc3MjE@._V1_Ratio0.7273_AL_.jpg",
        "https://imdb-api.com/images/original/MV5BODkxNGQ1NWYtNzg0Ny00Yjg3LThmZTItMjE2YjhmZTQ0ODY5XkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_Ratio0.7273_AL_.jpg",
        "https://imdb-api.com/images/original/MV5BNmMyMTY2YmEtZjM2ZS00ZWQ5LWE4YjEtOGMxOGZhY2RlZjJjXkEyXkFqcGdeQXVyNDM2OTEyOTM@._V1_Ratio0.7273_AL_.jpg"
      ],
      mainBackDrops: 'https://images.unsplash.com/photo-1509347528160-9a9e33742cdb?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=870&q=80',
      mainPlot: '-',
      wishList: new Array(),
      dataAPI: this.dummyItems,
      popularItems: this.dummyItems,
      mainData: {"id":"tt4566758","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BNDliY2E1MjUtNzZkOS00MzJlLTgyOGEtZDg4MTI1NzZkMTBhXkEyXkFqcGdeQXVyNjMwMzc3MjE@._V1_Ratio0.7273_AL_.jpg","title":"Mulan","description":"(2020)"},
      loadingPage: true,
      loadingSearch: false,
      errored: false
    } 
  },
  methods: {
    addWishListHandler(idItem) {
      if (!this.wishList.includes(idItem)) {
        this.wishList.push(idItem);
      }
    },
    removeWishListItemHandler(idItem) {
      this.wishList = this.wishList.filter(itemId => itemId != idItem);
    },
    async getSearchedTitle(keyword) {
      this.loadingSearch = true;
      await axios
        .get(`https://imdb-api.com/en/API/Search/k_34qll1u6/${keyword}`)
        .then(response => {
          this.dataAPI = response?.data?.results
        })
        .catch(error => {
          console.log(error)
          this.errored = true
        })
        .finally(() => this.loadingSearch = false)
    }
  },
  async mounted() {
    await axios
      .get('https://imdb-api.com/en/API/MostPopularTVs/k_34qll1u6')
      .then(response => {
        this.dataAPI = response?.data?.items?.slice(0,11)
        this.popularItems = response?.data?.items?.slice(0,6)
        this.mainData = response?.data?.items[0]
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
    console.log(this.mainData.id)
    await axios
      .get(`https://imdb-api.com/en/API/Title/k_34qll1u6/${this.mainData.id}/Posters,`)
      .then(response => {
        const posterArray = response?.data?.posters;
        if (posterArray.backdrops[0]?.link) {
          this.mainBackDrops = posterArray.backdrops[0]?.link;
        }
        if (posterArray.posters.length >= 3) {
          this.mainPosters = [];
          posterArray.posters.slice(0,3).map(poster => {
            this.mainPosters.push(poster.link);
          })
        } else if (posterArray.backdrops.length >= 3) {
          this.mainPosters = [];
          posterArray.backdrops.slice(0,3).map(poster => {
            this.mainPosters.push(poster.link);
          })
        }
        this.mainPlot = response?.data?.plot;
        console.log(response)
        
      })
      .catch(error => {
        console.log(error)
        this.errored = true
      })
      .finally(() => this.loadingPage = false);
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
}
body, html {
  padding: 0;
  margin: 0;
}
</style>
