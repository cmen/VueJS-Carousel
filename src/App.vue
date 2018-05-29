<template>
  <div id="app">
    <carousel>
      <carousel-slide v-for="n in slides" :index="n - 1" :key="n">
        <div style="position: absolute; left: 0; right:0; text-align: center; top:50%; color: #FFF; font-size: 16px;">Slide n°{{ n }}</div>
        <img src="./assets/example.jpeg" width="100%"/>
      </carousel-slide>
    </carousel>
    <button @click.prevent="addSlide">Ajouter un slide</button>
    <button @click.prevent="removeSlide">Supprimer un slide</button>
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
  methods: {
    addSlide () {
      this.slides++
    },
    removeSlide () {
      this.slides--
    }
  },
  components: {
    Carousel,
    CarouselSlide
  }
}
</script>
