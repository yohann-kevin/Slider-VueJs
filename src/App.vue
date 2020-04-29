<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :key="n" :index="n -1">
        <div class="contentImg">Article {{ n }}</div>
        <img :src="'https://i.picsum.photos/id/102'+ n +'/630/300.jpg'" width="100%">
      </carousel-slide>
      <!-- <carousel-slide>
        <div class="contentImg">aurevoir plop !</div>
        <img src="https://i.picsum.photos/id/1023/630/300.jpg" width="100%">
      </carousel-slide> -->
    </carousel>
    <button @click="addSlide()">Ajouter un slide</button>
    <button @click="removeSlide()">Retirer un slide</button>
  </div>
</template>

<script>
import Carousel from './components/carousel/Carousel'
import CarouselSlide from './components/carousel/CarouselSlide'

export default {
  name: 'App',
  data () {
    return {
      slides: 5
    }
  },
  components: {
    Carousel,
    CarouselSlide
  },
  methods: {
    addSlide () {
      this.slides++
    },
    removeSlide () {
      this.slides--
    }
  }
}
</script>

<style>
  .contentImg {
    position: absolute;
    left: 0;
    right: 0;
    text-align: center;
    top: 50%;
    color: #ffffff;
    font-size: 2rem;
  }
</style>
