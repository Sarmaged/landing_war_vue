<template>
  <div id="app">
    <locale />

    <div class="logo-wt z3">{{ $t('main.logo') }}</div>

    <div class="glob-title z1">
      <h1>{{ $t('main.h1') }}</h1>
      <img class="isNotMobile" :src="imgLoad('header_ru')" :alt="$t('main.h1')" />
      <img
        class="isMobile"
        :src="imgLoad('header_ru')"
        :srcset="`${imgLoad('header_ru_m')} 1x, ${imgLoad('header_ru_m@2x')} 2x`"
        :alt="`${$t('main.h1')} - mobile`"
      />
    </div>

    <div class="main">
      <div class="main-title z3" v-html="$t('main.title')"></div>

      <choose :items="chooseItems" />

      <gallery :images="galleryImages" />
    </div>

    <v-footer />
  </div>
</template>

<script>
import VFooter from './components/footer'
import Gallery from './components/gallery'
import Choose from './components/choose'
import Locale from './components/locale'

export default {
  name: 'App',
  data: () => ({
    chooseItems: [],
    galleryImages: []
  }),
  components: {
    VFooter,
    Gallery,
    Choose,
    Locale
  },
  computed: {
    currentLocale() {
      return this.$i18n.locale
    }
  },
  created() {
    const { images } = require('./gallery.json')
    this.galleryImages = images

    const chooseItems1 = require('./choose.json')
    this.chooseItems = chooseItems1
  },
  methods: {
    imgLoad(img) {
      const file = img.replace('_ru', `_${this.currentLocale}`)
      return require(`@/assets/img/headers/${file}.png`)
    }
  }
}
</script>

<style lang="scss" src="@/assets/css/app.scss" />
