<template>
  <div v-if="item" class="main" :style="{ backgroundImage: `url(${mainBackDrops})` }">
      <div class="main__description">
          <h1 class="main__title">{{ item.fullTitle }}</h1>
          <div v-if="mainPosters" class="main__posters main__posters--mobile">
            <div v-for="mainPoster in mainPosters" v-bind:key="mainPoster" class="main__poster">
              <img :src="mainPoster" :alt="item.fullTitle">
            </div>
        </div>
          <p>{{ mainPlot }}</p>
          <div class="main__description__actions">
              <Button class="main__description__watch">
                  <PlayCircleIcon /> Watch Now
              </Button>
              <Button v-if="listOfIdItems.includes(item.id)" :clickButton="() => onRemoveWishListItem(item.id)" class="main__description__remove">
                  <HeartIcon /> Remove from WishList
              </Button> 
              <Button v-else :clickButton="() => onAddWishListItem(item.id)" class="main__description__add">
                  <CardsHeartOutlineIcon /> Add to WishList
              </Button> 
          </div>
      </div>
      <div v-if="mainPosters" class="main__posters main__posters--desktop">
          <div v-for="mainPoster in mainPosters" v-bind:key="mainPoster" class="main__poster">
            <img :src="mainPoster" :alt="item.fullTitle">
          </div>
      </div>
  </div>
</template>

<script>
import Button from './Button.vue'
import HeartIcon from 'vue-material-design-icons/Heart.vue';
import CardsHeartOutlineIcon from 'vue-material-design-icons/HeartOutline.vue';
import PlayCircleIcon from 'vue-material-design-icons/PlayCircle.vue';

export default {
    name: 'Main',
    components: {
        Button,
        HeartIcon,
        CardsHeartOutlineIcon,
        PlayCircleIcon
    },
    props: {
      item: Object,
      listOfIdItems: Array,
      onRemoveWishListItem: Function,
      onAddWishListItem: Function,
      mainBackDrops: String,
      mainPosters: Array,
      mainPlot: String,
    },
}
</script>

<style scoped>

.main {
  display: flex;
  width: 100%;
  min-height: 100vh;
  align-items: center;
  padding: 1rem 4rem;
  box-sizing: border-box;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
  color: white;
  overflow-x: hidden;
}
.main::before {
    content: "";
    position: absolute;
    top: 0px;
    right: 0px;
    bottom: 0px;
    left: 0px;
    background-color: rgba(0,0,0,0.53);
}

.main__title {
  font-size: 2rem;
}

.main__description {
  width: 50%;
  z-index: 1;
}

.main__description__add svg,
.main__description__remove svg,
.main__description__watch svg {
  margin-right: 0.5rem;
}

.main__description__add,
.main__description__remove,
.main__description__watch {
  transition: transform 0.2s;
  color: #293241;
}

.main__description__watch {
  background-color: #fca311;
  font-weight: 700;
  margin-right: 1.5rem;
}

.main__description__add,
.main__description__remove {
  background-color: #ffffff;
}

.main__description__add {
  box-shadow: inset 0px 0px 0px 1px #fca311;
}

.main__description__remove {
  box-shadow: inset 0px 0px 0px 1px #f81111;
  color: #f81111;
}

.main__posters {
  position: relative;
  height: 100%;
  width: 50%;
  display: flex;
  align-items: center;
}

.main__posters--mobile {
  display: none;
}

.main__poster {
  width: 300px;
  height: 400px;
  position: absolute;
  border-radius: 10px;
  filter: drop-shadow(-6px 4px 4px rgba(0, 0, 0, 0.5));
  background-size: cover;
  background-repeat: no-repeat;
}

.main__poster img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: inherit;
}        

.main__poster:first-of-type {
  background-image: url("https://imdb-api.com/images/original/MV5BNDliY2E1MjUtNzZkOS00MzJlLTgyOGEtZDg4MTI1NzZkMTBhXkEyXkFqcGdeQXVyNjMwMzc3MjE@._V1_Ratio0.7273_AL_.jpg");
  transform: rotate(7deg);
  z-index: 1;
  left: 10%;
}

.main__poster:nth-child(2) {
  background-image: url("https://imdb-api.com/images/original/MV5BODkxNGQ1NWYtNzg0Ny00Yjg3LThmZTItMjE2YjhmZTQ0ODY5XkEyXkFqcGdeQXVyMTQxNzMzNDI@._V1_Ratio0.7273_AL_.jpg");
  transform: rotate(14deg);
  z-index: 2;
  left: 20%;
}

.main__poster:nth-child(3) {
  background-image: url("https://imdb-api.com/images/original/MV5BNmMyMTY2YmEtZjM2ZS00ZWQ5LWE4YjEtOGMxOGZhY2RlZjJjXkEyXkFqcGdeQXVyNDM2OTEyOTM@._V1_Ratio0.7273_AL_.jpg");
  transform: rotate(21deg);
  z-index: 3;
  left: 30%;
}

@media screen and (max-width: 992px) {
  .main__poster {
    width: 240px;
    height: 320px;
  }
}

@media screen and (max-width: 850px) {
  .main__description {
    width: 100%;
  }

  .main__posters--mobile {
    display: flex;
    height: 425px;
  }

  .main__posters--desktop {
    display: none;
  }

  .main__description__actions {
    margin-top: 2rem;
  }
}

@media screen and (max-width: 768px) {
  .main {
    padding: 1rem 2rem;
  }
}

@media screen and (max-width: 500px) {
  .main__poster {
    width: 210px;
    height: 280px;
  }
  .main__posters--mobile {
    height: 350px;
  }
}

@media screen and (max-width: 450px) {
  .main__poster {
    width: 210px;
    height: 280px;
  }
  .main__description__actions button {
    width: 100%;
    justify-content: center;
    font-size: 1rem;
  }

  .main__description__actions button:first-of-type {
    margin-bottom: 10px;
  }

  .main__description__actions button span {
    margin-right: 10px;
  }
}
</style>