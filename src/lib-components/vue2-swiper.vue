<script>
import { getParams } from "./utils/get-params";
import { initSwiper, mountSwiper } from "./utils/init-swiper";
import {
  needsScrollbar,
  needsNavigation,
  needsPagination,
  uniqueClasses,
  extend,
} from "./utils/utils";
import { renderLoop, calcLoopedSlides } from "./utils/loop";
import { getChangedParams } from "./utils/get-changed-params";
import { getChildren } from "./utils/get-children";
import { updateSwiper } from "./utils/update-swiper";
import { renderVirtual, updateOnVirtualData } from "./utils/virtual";

export default {
  name: "Swiper",
  props: {
    tag: {
      type: String,
      default: "div",
    },
    wrapperTag: {
      type: String,
      default: "div",
    },

    init: { type: Boolean, default: undefined },
    direction: { type: String, default: undefined },
    touchEventsTarget: { type: String, default: undefined },
    initialSlide: { type: Number, default: undefined },
    speed: { type: Number, default: undefined },
    cssMode: { type: Boolean, default: undefined },
    updateOnWindowResize: { type: Boolean, default: undefined },
    resizeObserver: { type: Boolean, default: undefined },
    nested: { type: Boolean, default: undefined },
    width: { type: Number, default: undefined },
    height: { type: Number, default: undefined },
    preventInteractionOnTransition: { type: Boolean, default: undefined },
    userAgent: { type: String, default: undefined },
    url: { type: String, default: undefined },
    edgeSwipeDetection: { type: [Boolean, String], default: undefined },
    edgeSwipeThreshold: { type: Number, default: undefined },
    freeMode: { type: Boolean, default: undefined },
    freeModeMomentum: { type: Boolean, default: undefined },
    freeModeMomentumRatio: { type: Number, default: undefined },
    freeModeMomentumBounce: { type: Boolean, default: undefined },
    freeModeMomentumBounceRatio: { type: Number, default: undefined },
    freeModeMomentumVelocityRatio: { type: Number, default: undefined },
    freeModeSticky: { type: Boolean, default: undefined },
    freeModeMinimumVelocity: { type: Number, default: undefined },
    autoHeight: { type: Boolean, default: undefined },
    setWrapperSize: { type: Boolean, default: undefined },
    virtualTranslate: { type: Boolean, default: undefined },
    effect: { type: String, default: undefined },
    breakpoints: { type: Object, default: undefined },
    spaceBetween: { type: Number, default: undefined },
    slidesPerView: { type: [Number, String], default: undefined },
    slidesPerColumn: { type: Number, default: undefined },
    slidesPerColumnFill: { type: String, default: undefined },
    slidesPerGroup: { type: Number, default: undefined },
    slidesPerGroupSkip: { type: Number, default: undefined },
    centeredSlides: { type: Boolean, default: undefined },
    centeredSlidesBounds: { type: Boolean, default: undefined },
    slidesOffsetBefore: { type: Number, default: undefined },
    slidesOffsetAfter: { type: Number, default: undefined },
    normalizeSlideIndex: { type: Boolean, default: undefined },
    centerInsufficientSlides: { type: Boolean, default: undefined },
    watchOverflow: { type: Boolean, default: undefined },
    roundLengths: { type: Boolean, default: undefined },
    touchRatio: { type: Number, default: undefined },
    touchAngle: { type: Number, default: undefined },
    simulateTouch: { type: Boolean, default: undefined },
    shortSwipes: { type: Boolean, default: undefined },
    longSwipes: { type: Boolean, default: undefined },
    longSwipesRatio: { type: Number, default: undefined },
    longSwipesMs: { type: Number, default: undefined },
    followFinger: { type: Boolean, default: undefined },
    allowTouchMove: { type: Boolean, default: undefined },
    threshold: { type: Number, default: undefined },
    touchMoveStopPropagation: { type: Boolean, default: undefined },
    touchStartPreventDefault: { type: Boolean, default: undefined },
    touchStartForcePreventDefault: { type: Boolean, default: undefined },
    touchReleaseOnEdges: { type: Boolean, default: undefined },
    uniqueNavElements: { type: Boolean, default: undefined },
    resistance: { type: Boolean, default: undefined },
    resistanceRatio: { type: Number, default: undefined },
    watchSlidesProgress: { type: Boolean, default: undefined },
    watchSlidesVisibility: { type: Boolean, default: undefined },
    grabCursor: { type: Boolean, default: undefined },
    preventClicks: { type: Boolean, default: undefined },
    preventClicksPropagation: { type: Boolean, default: undefined },
    slideToClickedSlide: { type: Boolean, default: undefined },
    preloadImages: { type: Boolean, default: undefined },
    updateOnImagesReady: { type: Boolean, default: undefined },
    loop: { type: Boolean, default: undefined },
    loopAdditionalSlides: { type: Number, default: undefined },
    loopedSlides: { type: Number, default: undefined },
    loopFillGroupWithBlank: { type: Boolean, default: undefined },
    loopPreventsSlide: { type: Boolean, default: undefined },
    allowSlidePrev: { type: Boolean, default: undefined },
    allowSlideNext: { type: Boolean, default: undefined },
    swipeHandler: { type: Boolean, default: undefined },
    noSwiping: { type: Boolean, default: undefined },
    noSwipingClass: { type: String, default: undefined },
    noSwipingSelector: { type: String, default: undefined },
    passiveListeners: { type: Boolean, default: undefined },
    containerModifierClass: { type: String, default: undefined },
    slideClass: { type: String, default: undefined },
    slideBlankClass: { type: String, default: undefined },
    slideActiveClass: { type: String, default: undefined },
    slideDuplicateActiveClass: { type: String, default: undefined },
    slideVisibleClass: { type: String, default: undefined },
    slideDuplicateClass: { type: String, default: undefined },
    slideNextClass: { type: String, default: undefined },
    slideDuplicateNextClass: { type: String, default: undefined },
    slidePrevClass: { type: String, default: undefined },
    slideDuplicatePrevClass: { type: String, default: undefined },
    wrapperClass: { type: String, default: undefined },
    runCallbacksOnInit: { type: Boolean, default: undefined },
    observer: { type: Boolean, default: undefined },
    observeParents: { type: Boolean, default: undefined },
    observeSlideChildren: { type: Boolean, default: undefined },
    a11y: { type: [Boolean, Object], default: undefined },
    autoplay: { type: [Boolean, Object], default: undefined },
    controller: { type: Object, default: undefined },
    coverflowEffect: { type: Object, default: undefined },
    cubeEffect: { type: Object, default: undefined },
    fadeEffect: { type: Object, default: undefined },
    flipEffect: { type: Object, default: undefined },
    hashNavigation: { type: [Boolean, Object], default: undefined },
    history: { type: [Boolean, Object], default: undefined },
    keyboard: { type: [Boolean, Object], default: undefined },
    lazy: { type: [Boolean, Object], default: undefined },
    mousewheel: { type: [Boolean, Object], default: undefined },
    navigation: { type: [Boolean, Object], default: undefined },
    pagination: { type: [Boolean, Object], default: undefined },
    parallax: { type: [Boolean, Object], default: undefined },
    scrollbar: { type: [Boolean, Object], default: undefined },
    thumbs: { type: Object, default: undefined },
    virtual: { type: [Boolean, Object], default: undefined },
    zoom: { type: [Boolean, Object], default: undefined },
  },
  data() {
    return {
      containerClasses: "swiper-container",
      virtualData: null,
      breakpointChanged: false,
      initializedRef: false,
      // swiperElRef: null,
      swiperRef: null,
      oldPassedParamsRef: null,
      slidesRef: { value: [] },
      oldSlidesRef: { value: [] },
      // nextElRef: null,
      // prevElRef: null,
      // paginationElRef: null,
      // scrollbarElRef: null,
    };
  },
  created() {
    const { params: swiperParams, passedParams } = getParams(this.$props);
    this.originalSlots = this.$slots;
    this.swiperParams = swiperParams;
    this.passedParams = passedParams;

    const { slides } = getChildren(
      this.originalSlots,
      this.slidesRef,
      this.oldSlidesRef
    );
    this.slidesRef = slides;
    this.oldPassedParamsRef = this.passedParams;
    this.oldSlidesRef = this.slidesRef;

    const onBeforeBreakpoint = () => {
      getChildren(this.originalSlots, this.slidesRef, this.oldSlidesRef);
      this.breakpointChanged = true;
    };

    this.swiperParams.onAny = (event, ...args) => {
      this.$emit(event, ...args);
    };

    Object.assign(this.swiperParams.on, {
      _beforeBreakpoint: onBeforeBreakpoint,
      _containerClasses(swiper, classes) {
        this.containerClasses = classes;
      },
    });

    this.swiperRef = initSwiper(this.swiperParams);
    this.swiperRef.loopCreate = () => {};
    this.swiperRef.loopDestroy = () => {};
    if (this.swiperParams.loop) {
      this.swiperRef.loopedSlides = calcLoopedSlides(
        this.slidesRef,
        this.swiperParams
      );
    }
    if (this.swiperRef.virtual && this.swiperRef.params.virtual.enabled) {
      this.swiperRef.virtual.slides = this.slidesRef;
      const extendWith = {
        cache: false,
        renderExternal: (data) => {
          this.virtualData = data;
        },
        renderExternalUpdate: false,
      };
      extend(this.swiperRef.params.virtual, extendWith);
      extend(this.swiperRef.originalParams.virtual, extendWith);
    }
  },
  updated() {
    // set initialized flag
    if (!this.initializedRef && this.swiperRef) {
      this.swiperRef.emitSlidesClasses();
      this.initializedRef = true;
    }
    // watch for params change
    const { passedParams: newPassedParams } = getParams(this.$props);

    const changedParams = getChangedParams(
      newPassedParams,
      this.oldPassedParamsRef,
      this.slidesRef,
      this.oldSlidesRef
    );
    this.oldPassedParamsRef = newPassedParams;

    if (
      (changedParams.length || this.breakpointChanged) &&
      this.swiperRef &&
      !this.swiperRef.destroyed
    ) {
      updateSwiper(
        this.swiperRef,
        this.slidesRef,
        newPassedParams,
        changedParams
      );
    }
    this.breakpointChanged = false;
  },
  watch: {
    virtualData() {
      this.$nextTick(() => {
        updateOnVirtualData(this.swiperRef);
      });
    },
  },
  mounted() {
    if (!this.$refs.swiperElRef) return;
    mountSwiper(
      {
        el: this.$refs.swiperElRef,
        nextEl: this.$refs.nextElRef,
        prevEl: this.$refs.prevElRef,
        paginationEl: this.$refs.paginationElRef,
        scrollbarEl: this.$refs.scrollbarElRef,
        swiper: this.swiperRef,
      },
      this.swiperParams
    );

    this.$emit("swiper", this.swiperRef);
  },
  beforeUnmount() {
    if (this.swiperRef && !this.swiperRef.destroyed) {
      this.swiperRef.destroy(true, false);
    }
  },
  methods: {
    renderSlides(slides) {
      if (this.swiperParams.virtual) {
        return renderVirtual(this.swiperRef, slides, this.virtualData);
      }
      if (
        !this.swiperParams.loop ||
        (this.swiperRef && this.swiperRef.destroyed)
      ) {
        slides.forEach((slide) => {
          if (!slide.props) slide.props = {};
          slide.props.swiperRef = this.swiperRef;
        });
        return slides;
      }
      return renderLoop(this.swiperRef, slides, this.swiperParams);
    },
  },
  render() {
    const h = this.$createElement;
    const { tag: Tag, wrapperTag: WrapperTag } = this.$props;
    const { slides, slots } = getChildren(
      this.originalSlots,
      this.slidesRef,
      this.oldSlidesRef
    );
    return h(
      Tag,
      {
        ref: "swiperElRef",
        class: uniqueClasses(this.containerClasses),
      },
      [
        slots["container-start"],
        needsNavigation(this.$props) && [
          h("div", { ref: "prevElRef", class: "swiper-button-prev" }),
          h("div", { ref: "nextElRef", class: "swiper-button-next" }),
        ],
        needsScrollbar(this.$props) &&
          h("div", { ref: "scrollbarElRef", class: "swiper-scrollbar" }),
        needsPagination(this.$props) &&
          h("div", { ref: "paginationElRef", class: "swiper-pagination" }),
        h(WrapperTag, { class: "swiper-wrapper" }, [
          slots["wrapper-start"],
          this.renderSlides(slides),
          slots["wrapper-end"],
        ]),
        slots["container-end"],
      ]
    );
  },
};
</script>
