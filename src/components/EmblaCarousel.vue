<script setup lang="ts">
import { ref, computed } from 'vue'
import { type EmblaOptionsType } from 'embla-carousel'
import emblaCarouselVue from 'embla-carousel-vue'

const props = defineProps<{ axis: 'x' | 'y' }>()

const dynamicFlexDirection = computed(() => (
  props.axis == 'x'
    ? 'flex-direction-row'
    : 'flex-direction-column'
))

const emblaOptions: EmblaOptionsType = {
  axis: props.axis,
  // slidesToScroll: 'auto',
  // containScroll: 'trimSnaps',
  // align: 'center', // default is center
  dragFree: true // Enables momentum scrolling
  // startIndex: 4
}

const [emblaNode, emblaApi] = emblaCarouselVue(ref(emblaOptions))

const clickSlide = (slideIndex: number) => {
  emblaApi.value?.scrollTo(slideIndex)
}
</script>

<template>
  <div
    ref="emblaNode"
    class="embla"
  >
    <div
      class="embla__container"
      :class="dynamicFlexDirection"
    >
      <div
        v-for="(slideIndex) in 10"
        :key="slideIndex - 1"
        class="embla__slide"
        @click="clickSlide(slideIndex - 1)"
      >
        {{slideIndex - 1}}<img src="./../assets/vue.svg" class="embla__slide__img" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.embla {
  --slide-width: 4em;
  --slide-height: 6em;
  margin: auto;
  --slide-spacing: 0.1em;
  --slide-size: 20%;
  overflow: hidden;
  height: 100%;
  cursor: grab;
  user-select: none;
}

.embla__container {
  backface-visibility: hidden;
  display: flex;
  touch-action: pan-x pinch-zoom;
  margin-bottom: calc(var(--slide-spacing) * -1);
  height: calc(var(--slide-spacing) + var(--slide-height));
}

.flex-direction-row {
  flex-direction: row;
}

.flex-direction-column {
  flex-direction: column;
}

.embla__slide {
  display: flex;
  flex: 0 0 var(--slide-size);
  /* min-height: 0; */
  padding-bottom: var(--slide-spacing);
}

/* stylelint-disable-next-line selector-class-pattern */
.embla__slide__img {
  width: var(--slide-width);
  height: var(--slide-height);
}

</style>
