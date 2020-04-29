<template>  
    <div class="carousel">
        <slot></slot>
        <button class="carousel__nav carousel__next" @click="next()">></button>
        <button class="carousel__nav carousel__prev" @click="prev()"><</button>
        <div class="carousel__pagintaion">
            <button v-for="n in slidesCount" :key="n" @click="goTo(n-1)" :class="{active: n-1 == index}"></button>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return {
            index: 0,
            slides: [],
            direction: 'right'
        }
    },
    computed: {
        slidesCount () {
            return this.slides.length
        }
    },
    watch: {
        slides (slides) {
            if(this.index >= this.slidesCount) {
                this.index = this.slidesCount - 1
            }
        }
    },
    methods: {
        next () {
            this.index++
            this.direction = 'right'
            if(this.index >= this.slidesCount) {
                this.index = 0
            }
        },
        prev () {
            this.index--
            this.direction = 'left'
            if(this.index < 0) {
                this.index = this.slidesCount - 1
            }
        },
        goTo (index) {
            this.direction = index > this.index ? 'right' : 'left'
            this.index = index
        }
    },
    mounted () {
        this.slides = this.$children
    },
}
</script>

<style>
  .carousel {
    position: relative;
    overflow: hidden;
  }

  .carousel__nav {
    position: absolute;
    margin-top: -35px;
    top: 50%;
    left: 10px;
    width: 63px;
    height: 63px;
    font-size: 3.3rem;
    color: rgba(239, 239, 239, 0.4);
    background-color: rgba(29, 29, 29, 0.3);
    border-radius: 15px;
    border: none;
  }

  .carousel__nav.carousel__next {
      right: 10px;
      left: auto;
  }

  .carousel__nav:hover {
    cursor: pointer;
    color: rgba(239, 239, 239, 0.6);
    background-color: rgba(29, 29, 29, 0.5);
  }

  .carousel__pagintaion {
    position: absolute;
    bottom: 10px;
    left: 0;
    right:0;
    text-align: center;
  }

  .carousel__pagintaion button{
    display: inline-block;
    width: 15px;
    height: 15px;
    background-color: #1d1d1d;
    opacity: 0.8;
    border: none;
    border-radius: 10px;
    margin: 3px;
  }

  .carousel__pagintaion button.active {
      background-color: #ffffff;
  }

  .carousel__pagintaion button:hover {
      cursor: pointer;
  }

</style>