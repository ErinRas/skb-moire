<template>
  <li class="catalog__item">
    <router-link class="catalog__pic" :to="{ name: 'product', params: { id } }">
      <img v-if="images[activeImgIdx] && images[activeImgIdx].file" :src="images[activeImgIdx].file.url" :alt="title" />
      <img v-else src="assets/no-image.jpg" />
    </router-link>

    <h3 class="catalog__title">
      <router-link :to="{ name: 'product', params: { id } }">
        {{ title }}
      </router-link>
    </h3>

    <span class="catalog__price"> {{ pricePretty }} ₽ </span>

    <ul class="colors colors--black">
      <li class="colors__item" v-for="color in colors" :key="color.id">
        <label class="colors__label" @click.prevent="changeImg(color.id)">
          <input class="colors__radio sr-only" type="radio" :name="'color-' + id" :value="color.color.code"
            :checked="color.id === activeImgId" />
          <span class="colors__value" :style="{ 'background-color': color.color.code }">
          </span>
        </label>
      </li>
    </ul>
  </li>
</template>

<script>
import numberFormat from '@/helpers/numberFormat.js'

export default {
  props: ['id', 'title', 'price', 'colors', 'images'],
  data() {
    return {
      activeImgIdx: 0,
    }
  },
  computed: {
    pricePretty() {
      return numberFormat(this.price)
    },
    activeImgId() {
      return this.colors[this.activeImgIdx].id
    },
  },
  methods: {
    changeImg(val) {
      const idx = this.colors.findIndex((item) => item.id === val)
      this.activeImgIdx = idx
    },
  },
}
</script>
