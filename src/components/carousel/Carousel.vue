<template>
    <div class="carousel">
        <slot></slot>
        <button class="carousel-nav carousel-prev" @click.prevent="prev"></button>
        <button class="carousel-nav carousel-next" @click.prevent="next"></button>
        <div class="carousel-pagination">
            <button v-for="n in slidesCount" @click="goto(n-1)" :class="{active: n-1 == index}" :key="n"></button>
        </div>
    </div>
</template>

<script>
export default {
  name: 'Carousel',
  data () {
    return {
      index: 0,
      slides: [],
      direction: 'right'
    }
  },
  watch: {
    slides (slides) {
      if (this.index >= this.slidesCount) {
        this.index = this.slidesCount - 1
      }
    }
  },
  computed: {
    slidesCount () { return this.slides.length }
  },
  methods: {
    prev () {
      this.index--
      this.direction = 'left'

      if (this.index < 0) {
        this.index = this.slidesCount - 1
      }
    },
    next () {
      this.index++
      this.direction = 'right'

      if (this.index >= this.slidesCount) {
        this.index = 0
      }
    },
    goto (index) {
      this.direction = index > this.index ? 'right' : 'left'
      this.index = index
    }
  },
  mounted () {
    this.slides = this.$children
  }
}
</script>

<style>
    .carousel {
        position: relative;
        overflow: hidden;
    }

    .carousel-nav {
        position: absolute;
        top: 50%;
        margin-top: -31px;
        left: 10px;
        background: url('prev.png');
        width: 63px;
        height: 63px;
    }

    .carousel-nav.carousel-next {
        right: 10px;
        left: auto;
        background: url('next.png');
    }

    .carousel-pagination {
        position: absolute;
        bottom: 10px;
        left: 0;
        right: 0;
        text-align: center;
    }

    .carousel-pagination button {
        display: inline-block;
        width: 20px;
        height: 20px;
        background-color: #000;
        opacity: 0.8;
        border-radius: 10px;
        margin: 0 2px;
    }

    .carousel-pagination button.active {
        background-color: #FFF;
    }
</style>
