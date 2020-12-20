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
          'images/slider/GoofGroup1.jpg',
          'images/slider/Group1.jpg',
          'images/slider/TSGroup2.jpg',
          'images/slider/TSgroup3.jpg',
          'images/slider/TSgroup4.jpg',
          'images/slider/TSgroup5.jpg',
          'images/slider/TSgroup6.jpg',
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
