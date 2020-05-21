<template>
  <div class="gallery z10">
    <transition name="fade">
      <div class="gallery-big" v-if="show" @click="close">
        <div class="gallery-big-image" @click.stop>
          <img :src="bigImage" alt="" />
          <div class="gallery-pagination">
            <a
              v-for="(image, x) in images"
              :key="x"
              href="#"
              :class="{ active: image.id === active }"
              @click.prevent="showBig(image)"
            >
              <img :src="src(image)" :alt="x" />
            </a>
          </div>
          <a href="#" @click.prevent="next" class="gallery-big-next"></a>
          <a href="#" @click.prevent="prev" class="gallery-big-prev"></a>
        </div>
        <a href="#" @click.prevent="close" class="gallery-big-close"></a>
      </div>
    </transition>
    <div class="gallery-title isMobile">
      {{ $t('gallery.title') }}
    </div>
    <div class="gallery-pagination">
      <a v-for="(image, x) in images" :key="x" href="#" @click.prevent="showBig(image)">
        <img :src="src(image)" :alt="x" />
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },
  data: () => ({
    show: false,
    active: null,
    bigImage: null
  }),
  created() {
    window.addEventListener('keyup', this.keyUp)
  },
  destroyed() {
    window.removeEventListener('keyup', this.keyUp)
  },
  methods: {
    keyUp(event) {
      if (!this.show) return

      switch (event.keyCode) {
        case 27: // esc
          return this.close()
        case 37: // left
          return this.prev()
        case 39: // right
          return this.next()
      }
    },
    src({ small, path, type }) {
      return require(`@/${path}${small}.${type}`)
    },
    showBig({ id, big, path, type }) {
      this.show = true
      this.active = id
      this.bigImage = require(`@/${path}${big}.${type}`)
    },
    getIndex(active) {
      return {
        length: this.images.length - 1,
        index: this.images.findIndex(item => item.id === active)
      }
    },
    prev() {
      const { length, index } = this.getIndex(this.active)
      const active = index <= 0 ? length : index - 1
      this.showBig(this.images[active])
    },
    next() {
      const { length, index } = this.getIndex(this.active)
      const active = index >= length ? 0 : index + 1
      this.showBig(this.images[active])
    },
    close() {
      this.show = false
      this.active = null
      this.bigImage = null
    }
  }
}
</script>

<style lang="scss" src="./_.scss" scoped />
