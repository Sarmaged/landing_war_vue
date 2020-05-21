<template>
  <div class="locale z3">
    <div :class="['locale-selected', { 'locale-selected__show': isShowLangList }]" @click="showLangList">
      <img :src="src(currentLocale)" :alt="currentLocale" />
    </div>
    <transition name="fade">
      <div class="locale-changer" v-if="isShowLangList">
        <div
          :class="['locale-changer-item', { 'locale-changer-item__active': currentLocale === locale }]"
          v-for="(locale, x) in langs"
          :key="x"
          @click="setLocal(locale)"
        >
          <img :src="src(locale)" :alt="locale" /> {{ $t(`langs.${locale}`) }}
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data: () => ({
    langs: ['ru', 'tr'],
    isShowLangList: false
  }),
  computed: {
    currentLocale() {
      return this.$i18n.locale
    }
  },
  methods: {
    showLangList() {
      this.isShowLangList = true
    },
    setLocal(locale) {
      if (!locale) return
      this.isShowLangList = false

      if (this.currentLocale === locale) return
      this.$i18n.locale = locale
    },
    src(lang) {
      if (!lang) return
      return require(`@/assets/img/flags/${lang}.png`)
    }
  }
}
</script>

<style lang="scss" src="./_.scss" scoped />
