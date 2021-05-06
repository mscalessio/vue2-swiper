## Swiper Vue.js version 2 Components

This version of Swiper is a porting of the [original Swiper Vue.js components](https://github.com/nolimits4web/swiper) and is compatible with Vue.js version 2 and above.

## Installation

Swiper Vue.js plugin is available only via NPM:

```
  npm i swiper @mscalessio/vue2-swiper
```

## Usage

`@mscalessio/vue2-swiper` exports 2 components: `Swiper` and `SwiperSlide` like the original plugin:

```html
<template>
  <swiper
    :slides-per-view="3"
    :space-between="50"
    @swiper="onSwiper"
    @slideChange="onSlideChange"
  >
    <swiper-slide>Slide 1</swiper-slide>
    <swiper-slide>Slide 2</swiper-slide>
    <swiper-slide>Slide 3</swiper-slide>
    ...
  </swiper>
</template>
<script>
  // Import Swiper Vue.js version 2 components
  import { Swiper, SwiperSlide } from '@mscalessio/vue2-swiper';

  // Import Swiper styles from the original package
  import 'swiper/swiper.scss';
  export default {
    components: {
      Swiper,
      SwiperSlide,
    },
    methods: {
      onSwiper(swiper) {
        console.log(swiper);
      },
      onSlideChange() {
        console.log('slide change');
      },
    },
  };
</script>
```