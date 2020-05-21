<template>
  <div class="choose-blocks z3" v-if="items.length">
    <a
      @click.prevent
      href="#"
      v-for="(item, x) in items"
      :class="['choose-block', `choose-block__${item.type}`]"
      :key="x"
    >
      <div :class="['choose-block-icon', `choose-block-icon__${item.type}`]">
        <img :src="src(item.image)" :alt="item.type" />
      </div>
      <div class="choose-block-title">
        {{ $t(`main.block.list[${x}].type`) }}
        <strong>{{ $t(`main.block.list[${x}].model`) }}</strong>
      </div>
      <div class="choose-block-description">
        {{ $t('main.block.description') }}
      </div>
    </a>

    <div class="choose-or">
      {{ $t('main.block.or') }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    items: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    src(image) {
      return require(`@/assets/img/${image}`)
    }
  }
}
</script>

<style lang="scss" src="./_.scss" scoped />
