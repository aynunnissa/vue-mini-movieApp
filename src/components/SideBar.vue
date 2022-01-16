<template>
  <nav class="sidenav">
    <ul class="sidenav__menus">
      <li class="sidenav__menu" title="Not available"><AccountCircleIcon /></li>
      <li class="sidenav__menu"><hr /></li>
      <li class="sidenav__menu" title="Not available"><HomeIcon /></li>
      <li class="sidenav__menu active"><a href=""><TelevisionClassicIcon /></a></li>
      <li class="sidenav__menu" title="Not available"><MovieIcon /></li>
    </ul>
    <ul class="sidenav__menus">
      <li class="sidenav__menu sidenav__menu__favorite">
          <HeartIcon /><span class="sidenav__menu__totalWishList">{{ totalWishList }}</span>
      </li>
    </ul>
  </nav>
</template>

<script>
import HomeIcon from 'vue-material-design-icons/Home.vue';
import AccountCircleIcon from 'vue-material-design-icons/AccountCircle.vue';
import TelevisionClassicIcon from 'vue-material-design-icons/TelevisionClassic.vue';
import MovieIcon from 'vue-material-design-icons/Movie.vue';
import HeartIcon from 'vue-material-design-icons/Heart.vue';

export default {
    name: 'SideBar',
    components: {
        HomeIcon,
        AccountCircleIcon,
        TelevisionClassicIcon,
        MovieIcon,
        HeartIcon
    },
    props: {
        totalWishList: {
            type: Number,
            default: 0
        }
    }
}
</script>


<style scoped>
.sidenav {
  width: 65px;
  height: 100vh;
  position: fixed;
  top: 0;
  background-color: #293241;
  display: flex;
  align-content: space-between;
  flex-wrap: wrap;
}

.sidenav__menu {
  margin-left: 0.5rem;
  margin-right: 0.5rem;
}

.sidenav__menu hr {
  border: none;
  border-top: 1px solid white;
}

.sidenav__menus {
  list-style-type: none;
  color: white;
  padding: 0;
  width: 100%;
  text-align: center;
  cursor: pointer;
}

.sidenav__menus li {
  margin-top: 1.5rem;
}

.sidenav__menu a {
  text-decoration: none;
  color: inherit;
}

.sidenav__menu a svg {
  width: 1.8rem;
  height: 1.8rem;
}
.sidenav__menu.sidenav__menu__favorite {
  position: relative;
  margin-bottom: 1.5rem;
}

.sidenav__menu__totalWishList {
  background-color: #f81111;
  top: -0.5rem;
  left: 1.8rem;
  position: absolute;
  border-radius: 20px;
  min-width: 1.2rem;
  height: 1.2rem;
  font-size: 0.8rem;
  box-shadow: -0.6px 1px 0px rgba(255, 255, 255, 0.8);
  display: flex;
  align-items: center;
  justify-content: center;
}

.active {
  background-color: #fca311;
  color: #293241;
  border-radius: 5px;
  padding-top: 0.3rem;
}
</style>