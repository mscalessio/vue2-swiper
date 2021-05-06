<script>
import { uniqueClasses } from "./utils/utils";
export default {
  name: "SwiperSlide",
  props: {
    tag: {
      type: String,
      default: "div",
    },
    swiperRef: Object,
    zoom: { type: Boolean, default: undefined },
    virtualIndex: {
      type: [String, Number],
      default: undefined,
    },
  },
  data() {
    return {
      slideElRef: null,
      slideClasses: "swiper-slide",
    };
  },
  created() {
    this.eventAttached = false;
  },
  computed: {
    slideData() {
      return {
        isActive:
          this.slideClasses.indexOf("swiper-slide-active") >= 0 ||
          this.slideClasses.indexOf("swiper-slide-duplicate-active") >= 0,
        isVisible: this.slideClasses.indexOf("swiper-slide-visible") >= 0,
        isDuplicate: this.slideClasses.indexOf("swiper-slide-duplicate") >= 0,
        isPrev:
          this.slideClasses.indexOf("swiper-slide-prev") >= 0 ||
          this.slideClasses.indexOf("swiper-slide-duplicate-prev") >= 0,
        isNext:
          this.slideClasses.indexOf("swiper-slide-next") >= 0 ||
          this.slideClasses.indexOf("swiper-slide-duplicate-next") >= 0,
      };
    },
  },
  mounted() {
    if (!this.swiperRef) return;
    this.swiperRef.on("_slideClass", this.updateClasses);
    this.eventAttached = true;
  },
  beforeUpdate() {
    if (this.eventAttached || !this.swiperRef) return;
    this.swiperRef.on("_slideClass", this.updateClasses);
    this.eventAttached = true;
  },
  updated() {
    if (!this.slideElRef) return;
    if (this.swiperRef.destroyed) {
      if (this.slideClasses !== "swiper-slide") {
        this.slideClasses = "swiper-slide";
      }
    }
  },

  beforeUnmount() {
    if (!this.swiperRef) return;
    this.swiperRef.off("_slideClass", this.updateClasses);
  },
  methods: {
    updateClasses(swiper, el, classNames) {
      if (el === this.slideElRef) {
        this.slideClasses = classNames;
      }
    },
  },
  render() {
    const h = this.$createElement;
    const props = this.$props;
    return h(
      props.tag,
      {
        class: uniqueClasses(`${this.slideClasses}`),
        ref: this.slideElRef,
        "data-swiper-slide-index": props.virtualIndex,
      },
      props.zoom
        ? h(
            "div",
            {
              class: "swiper-zoom-container",
              "data-swiper-zoom":
                typeof props.zoom === "number" ? props.zoom : undefined,
            },
            this.$slots.default && this.$slots.default
          )
        : this.$slots.default && this.$slots.default
    );
  },
};
</script>
