<template lang="pug">
.picture_grid
  .header
    .h2.highlight {{data.title}}
  .benefits_grid
    .benefits_container(v-for="(item, index) in data.cards")
      //- nuxt-link(v-if="item.link" :to="item.link")
      img(:src="require(`~/assets/images/${item.image}`)").faded_out
      .benefits_container__title
        .h1.faded_out {{++index}}
        .h4.faded_out {{item.title}}
      .h5(v-if="item.description") {{item.description}}
</template>

<script>
import { add_class_on_focus } from '@/assets/scripts/dom_utils';

export default {
  props: ['data'],
  mounted: () => {
    add_class_on_focus({
      ['.faded_out']: 'fade_in',
    });
  },
};
</script>

<style lang="sass" scoped>
.picture_grid
  padding: clamp(25px, 5vw, 50px)

  .header
    // text-align: center
    .h2
      color: $fg_dark_title
      margin: clamp(25px, 10vw, 100px) 0
      font-size: clamp(13px, 3vw, 40px)

  .benefits_grid
    display: grid
    @media (min-width: 601px)
      grid-template-columns: auto auto auto

    grid-gap: 50px
    .benefits_container
      position: relative
      overflow: hidden
      height: 350px

      img,
      .h5
        height: 80%
        aspect-ratio: 16 / 9

      img
        display: block
        width: 100%
        object-fit: cover
      &__title, .h5
        position: absolute
      &__title
        left: 0
        bottom: 0
        display: grid
        grid-template-columns: auto auto
        place-items: center
        align-items: end
        z-index: 9
        grid-gap: 15px
        .h1
          font-size: clamp(100px, 20vw, 130px)
          font-weight: 900
          -webkit-text-stroke-width: 2px
          // -webkit-text-stroke-color: grey
          -webkit-text-stroke-color: lighten(black, 35)
          -webkit-text-fill-color: transparent
        .h4
          color: $fg_dark_title
          text-transform: capitalize
          margin-top: 25px
          line-height: 4
          font-size: clamp(16px, 2.2vw, 20px)
      .h5
        padding: 25px
        // background: $yy_yellow
        background: linear-gradient($yy_yellow, 90%, transparent)
        // max-width: 100%
        width: 100%
        // opacity: 0.9
        color: $fg_dark_text
        font-weight: 600
        font-size: clamp(12px, 2.1vw, 16px)
        top: 0
        left: 0
        transform: translateY(-100%)
        transition: transform 500ms
      &:hover .h5
        transform: translateY(0)
</style>
