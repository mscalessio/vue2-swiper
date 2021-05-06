<script>
import Vue from "vue";
// Uncomment import and local "components" registration if library is not registered globally.
import { Swiper, SwiperSlide } from "@/entry.esm";

// Import Swiper styles
  import 'swiper/swiper.scss';

export default Vue.extend({
  name: "ServeDev",
  components: {
    Swiper,
    SwiperSlide
  },
  methods: {
    onSwiper(swiper) {
      console.log(swiper);
    },
    onSlideChange() {
      console.log("slide change");
    },
  },
});
</script>

<template>
  <div id="app">
    <swiper
      :slides-per-view="3"
      :space-between="50"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
    >
      <swiper-slide>Slide 1</swiper-slide>
      <swiper-slide>Slide 2</swiper-slide>
      <swiper-slide>Slide 3</swiper-slide>
    </swiper>
  </div>
</template>
