<template>
    <div class="carousel__item__innerCard" :title="item.title">
        <div class="carousel__item__poster">
          <img :src="item.image" :alt="item.title">
        </div>
        <div class="carousel__item__description">
            <div class="carousel__item__info">
                <p class="carousel__item__info__title">{{ title }}</p>
                <p v-if="item.year" class="carousel__item__info__year">{{ item.year }}</p>
                <p v-if="item.description" class="carousel__item__info__year">{{ item.description }}</p>
            </div>
            <div class="carousel__item__favorite">
                <HeartIcon v-if="listOfIdItems.includes(item.id)" @click="onRemoveWishListItem(item.id)" />
                <CardsHeartOutlineIcon v-else @click="onAddWishListItem(item.id)" />
            </div>
        </div>
    </div>
</template>

<script>

import HeartIcon from 'vue-material-design-icons/Heart.vue';
import CardsHeartOutlineIcon from 'vue-material-design-icons/HeartOutline.vue';

export default {
  name: 'Card',
  components: {
    HeartIcon,
    CardsHeartOutlineIcon,
  },
  data() {
    return {
      title: this.item.title
    }
  },
  props: {
    item: {
      type: Object,
      default() {
        return {"id":"tt4566758","resultType":"Title","image":"https://imdb-api.com/images/original/MV5BNDliY2E1MjUtNzZkOS00MzJlLTgyOGEtZDg4MTI1NzZkMTBhXkEyXkFqcGdeQXVyNjMwMzc3MjE@._V1_Ratio0.7273_AL_.jpg","title":"Mulan","description":"(2020)"}
      }
    },
    listOfIdItems: {
      type: Array,
      default() {return []}
    },
    onRemoveWishListItem: Function,
    onAddWishListItem: Function
  },
  mounted() {
    this.title = (this.item.title.length <= 20) ? this.item.title : this.item.title.slice(0,15) + '...';
    
  }
}
</script>

<style scoped>
.carousel__item__innerCard {
  height: 100%;
  width: 100%;
}

.carousel__item__poster {
  background-color: blue;
  height: 85%;
  width: 100%;
  border-radius: 5px;
}

.carousel__item__poster img {
  height: 100%;
  width: 100%;
  object-fit: cover;
  border-radius: inherit;
}

.carousel__item__description {
  max-height: 25%;
  width: 100%;
  padding-top: 10px;
  box-sizing: border-box;
  display: flex;
  justify-content: space-between;
}

.carousel__item__info p {
  margin: 0;
  line-height: 1.5rem;
}

.carousel__item__info__title {
  font-weight: 600;
  color: #293241;
}

.carousel__item__info__year {
  font-weight: 600;
  color: #777778;
  font-size: 0.8rem;
}

.carousel__item__favorite {
  cursor: pointer;
  color: #fca311;
}

</style>