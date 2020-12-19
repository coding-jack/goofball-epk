<template>
  <div class="band-photos mb-4">
    <h3 class="heading mb-3">Photos</h3>
    <b-carousel
      id="carousel-1"
      v-model="slide"
      :interval="7500"
      controls
      :fade="true"
      :indicators="false"
      background="#ababab"
      img-width="1024"
      img-height="480"
      style="text-shadow: 1px 1px 2px #333;"
      @sliding-start="onSlideStart"
      @sliding-end="onSlideEnd"
    >

      <!-- Slides with image only -->
      <b-carousel-slide
        v-for="image in images"
        :key="image.id"
        :img-src="image" />
    </b-carousel>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        slide: 0,
        sliding: null,
        images: [
          'images/slider/group.jpg',
          'images/slider/jackson-1.jpg',
          'images/slider/pieter.jpg',
          'images/slider/steve.jpg',
          'images/slider/kevin.jpg',
          'images/slider/dalton.jpg',
          'images/slider/jackson.jpg',
          'images/slider/pieter-2.jpg',
          'images/slider/kevin-solo.jpg',
          'images/slider/steve-2.jpg',
          'images/slider/dalton-steve.jpg',
          'images/slider/pieter-3.jpg',
          'images/slider/kevin-2.jpg'
        ]
      }
    },
    methods: {
      onSlideStart(slide) {
        this.sliding = true
      },
      onSlideEnd(slide) {
        this.sliding = false
      }
    }
  }
</script>
