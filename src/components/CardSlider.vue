<template>
  <agile :slidesToShow="4" :dots="false" :options="myOptions">
    <div v-for="item in items" v-bind:key="item.id" class="slide">
      <div class="carousel__item">
          <div class="carousel__item__card">
            <Card
                :onAddWishListItem="onAddWishListItem"
                :onRemoveWishListItem="onRemoveWishListItem"
                :listOfIdItems="listOfIdItems"
                :item="item"
            />
          </div>
      </div>
    </div>
  </agile>
</template>

<script>
import { VueAgile } from 'vue-agile';
import Card from './Card.vue';

export default {
    name: 'CardSlider',
    components: {
        agile: VueAgile,
        Card
    },
    data() {
        return {
            myOptions: {
            navButtons: true,
            slidesToShow: "4",
            responsive: [
                {
                    breakpoint: 1100,
                    settings: {
                        slidesToShow: "4"
                    }
                },
                {
                    breakpoint: 850,
                    settings: {
                        slidesToShow: "3"
                    }
                },
                {
                    breakpoint: 576,
                    settings: {
                        slidesToShow: "2"
                    }
                },
                {
                    breakpoint: 0,
                    settings: {
                        slidesToShow: "1"
                    }
                }
            ]
            }
        }
    },
    props: {
        items: Array,
        onRemoveWishListItem: Function,
        onAddWishListItem: Function,
        listOfIdItems: Array,
    }
}
</script>

<style>
.carousel {
    width: 100%;
    margin-left: 65px;
}

.agile__actions {
    display: flex;
    align-items: center;
}

.agile__nav-button {
    background-color: #293241;
    border-radius: 50%;
    border: none;
    color: #fff;
    cursor: pointer;
    font-size: 24px;
    position: absolute;
    top: 0;
    bottom: 0;
    margin-top: auto;
    margin-bottom: auto;
    transition-duration: .3s;
    width: 40px;
    height: 40px;
}

.agile__nav-button:hover {
    background-color: rgba(#000, .5);
    opacity: 1;
}

.agile__nav-button--prev {
    left: 0;
}

.agile__nav-button--next {
    right: 0;
}


.agile .slide .carousel__item {
    height: fit-content;
    padding: 15px;
    box-sizing: border-box;
    width: 100%;
}

.agile .slide .carousel__item .carousel__item__card {
    height: 400px;
    width: 100%;
    background: rgba(255, 255, 255, 0.3);
    border: 2px solid rgba(255, 255, 255, 0.7);
    backdrop-filter: blur(20px);
    /* Note: backdrop-filter has minimal browser support */
    border-radius: 15px;
    padding: 20px;
    box-sizing: border-box;
}
</style>