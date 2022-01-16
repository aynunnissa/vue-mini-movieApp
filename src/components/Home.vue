<template>
    <div v-if="loadingPage" class="loadingPage">
      <div>
        <img :src="require(`@/assets/loading.svg`)" alt="Loading...">
        <p>Loading...</p>
      </div>
    </div>
    <div v-else-if="errored" class="errorPage">
      <div>
        <div class="image">
          <img :src="require(`@/assets/error.svg`)" alt="Error...">
        </div>
        <p>We're not able to retrieve the information today due to limited data request, please try again tomorrow</p>
      </div>
    </div>
    <section v-else class="home">
        <Main 
          :onAddWishListItem="onAddWishListItem"
          :onRemoveWishListItem="onRemoveWishListItem"
          :listOfIdItems="wishListItem"
          :item="mainData"
          :mainPosters="mainPosters"
          :mainBackDrops="mainBackDrops"
          :mainPlot="mainPlot"
        />
        <section class="popular">
          <h1 class="home__section-title">Most Popular TVs</h1>
          <CardSlider 
            :items="popularItems"
            :onAddWishListItem="onAddWishListItem"
            :onRemoveWishListItem="onRemoveWishListItem"
            :listOfIdItems="wishListItem"
          />
        </section>
        <section class="searchSection">
            <h1 class="home__section-title">Find Your Favorites</h1>
            <form action="" @submit="onSubmitSearch">
              <div class="inputField">
                  <input type="text" v-model="search" placeholder="Search Your Favorite...">
                  <button type="submit"><MagnifyIcon /></button>
              </div>
            </form>
            <div v-if="loadingSearch" class="loadingSearch">
              <div>
                <img :src="require(`@/assets/loading.svg`)" alt="Searching...">
                <p>Searching...</p>
              </div>
            </div>
            <CardList 
              v-else
              :onAddWishListItem="onAddWishListItem"
              :onRemoveWishListItem="onRemoveWishListItem"
              :listOfIdItems="wishListItem"
              :items="items"
            />
        </section>
    </section>
</template>

<script>
import Main from './Main.vue';
import CardList from './CardList.vue';
import CardSlider from './CardSlider.vue';
import MagnifyIcon from 'vue-material-design-icons/Magnify.vue';

export default {
  name: 'Home',
  components: {
    Main,
    CardList,
    CardSlider,
    MagnifyIcon
  },
  data () {
    return {
      search: null,
    }
  },
  props: {
    items: Array,
    popularItems: Array,
    onRemoveWishListItem: Function,
    onAddWishListItem: Function,
    onSearch: Function,
    wishListItem: Array,
    mainData: Object,
    loadingSearch: Boolean,
    loadingPage: Boolean,
    errored: Boolean,
    mainBackDrops: String,
    mainPosters: Array,
    mainPlot: String,
  },
  methods: {
    onSubmitSearch(e) {
      e.preventDefault();
      this.onSearch(this.search);
    },
  }
}
</script>

<style scoped>
.home {
  background-color: aliceblue;
  height: 100vh;
  max-height: 100vh;
  margin-left: 65px;
}

.loadingPage, .loadingSearch, .errorPage {
  margin-left: 65px;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

.loadingPage p, .loadingSearch p, .errorPage p {
  text-align: center;
}

.searchSection .loadingSearch {
  margin-left: 0;
  height: 50vh;
}
.errorPage {
  padding: 0px 25px;
}
.errorPage .image {
  display: flex;
  justify-content: center;
}
.errorPage img {
  width: 50%;
  height: auto;
}

.home__section-title {
  font-size: 2rem;
}

.popular {
  padding: 50px;
  box-sizing: border-box;
  background-color:#E7ECF4;
}

.searchSection {
  padding: 50px;
  min-height: 50vh;
}

.inputField {
  margin-bottom: 2rem;
  display: flex;
  width: 100%;
  background-color: red;
  border-radius: 10px;
  background-color: #f2f2f2;
  align-items: center;
  padding-left: 10px;
  box-sizing: border-box;
}

.inputField input {
  width: 100%;
  box-sizing: border-box;
  padding: 10px;
  border: none;
  background-color: transparent;
}

.inputField button {
  border: none;
  background-color: transparent;
}

.inputField input:focus {
  outline: none;
}

@media screen and (max-width: 450px) {
  .popular, .searchSection {
    padding: 50px 25px;
  }
}
</style>