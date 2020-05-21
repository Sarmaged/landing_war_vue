<template>
  <div class="locale z3">
    <div :class="['locale-selected', { 'locale-selected__show': isShowLangList }]" @click="showLangList">
      <img :src="src($i18n.locale)" alt="" />
    </div>
    <transition name="fade">
      <div class="locale-changer" v-if="isShowLangList">
        <div
          :class="['locale-changer-item', { 'locale-changer-item__active': $i18n.locale === lang }]"
          v-for="(lang, i) in langs"
          :key="`Lang${i}`"
          @click="setLocal(lang)"
        >
          <img :src="src(lang)" alt="" /> {{ $t(`langs.${lang}`) }}
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
export default {
  data: () => ({
    selected: 'ru',
    isShowLangList: false,
    langs: ['ru', 'tr']
  }),
  methods: {
    showLangList() {
      this.isShowLangList = true
    },
    setLocal(lang) {
      if (!lang) return
      this.isShowLangList = false

      if (this.$i18n.locale === lang) return
      this.$i18n.locale = lang
    },
    src(lang) {
      if (!lang) return
      return require(`@/assets/img/flags/${lang}.png`)
    }
  }
}
</script>

<style lang="scss" src="./_.scss" scoped />
