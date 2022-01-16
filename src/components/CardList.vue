<template>
    <div class="cardlist">
        <div v-for="item in items" v-bind:key="item.id" class="item">
            <Card 
                :onAddWishListItem="onAddWishListItem"
                :onRemoveWishListItem="onRemoveWishListItem"
                :listOfIdItems="listOfIdItems"
                :item="item"
            />
        </div>
    </div>
</template>

<script>
import Card from './Card.vue'

export default {
  name: 'CardList',
  components: {
      Card
  },
  props: {
    items: Array,
    onRemoveWishListItem: Function,
    onAddWishListItem: Function,
    listOfIdItems: Array,
  },
}
</script>

<style scoped>
.cardlist {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
}

.item {
  width: 200px;
  height: 300px;
  margin-bottom: 50px;
}

@media screen and (max-width: 576px) {
  .cardlist .item {
    width: 160px;
    height: auto;
  }
}

@media screen and (max-width: 485px) {
  .cardlist .item {
    width: 100%;
    height: auto;
  }
}
</style>