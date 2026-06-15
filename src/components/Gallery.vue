<template>
  <div>
    <div class="gallery-grid grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 gap-3">
      <div v-for="(img, idx) in images" :key="idx" class="cursor-pointer">
        <div class="thumb fade-up" :style="{ 'animation-delay': (idx * 80) + 'ms' }">
          <img :src="img" alt="gallery image" class="thumb-img" @click="open(idx)" />
        </div>
      </div>
    </div>

    <div v-if="selected !== null" class="fixed inset-0 bg-black/70 flex items-center justify-center z-50" @click.self="close">
      <div class="max-w-[90%] max-h-[90vh] p-4">
        <img :src="images[selected]" class="max-h-[80vh] w-auto mx-auto rounded" />
        <div class="flex justify-between mt-2">
          <button class="px-3 py-1 bg-white/20 text-white rounded" @click.stop="prev">Prev</button>
          <button class="px-3 py-1 bg-white/20 text-white rounded" @click.stop="next">Next</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PortfolioGallery',
  props: {
    images: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      selected: null
    };
  },
  methods: {
    open(i) { this.selected = i; },
    close() { this.selected = null; },
    prev() { if (this.selected > 0) this.selected--; },
    next() { if (this.selected < this.images.length - 1) this.selected++; }
  }
}
</script>

<style scoped>
.gallery-grid img { display: block; }
.gallery-grid img:hover { transform: scale(1.02); transition: transform .15s ease; }
.gallery-grid div { overflow: hidden; }
/* thumbnail: fixed aspect ratio (4:3) and cover */
.thumb { position: relative; padding-top: 75%; overflow: hidden; border-radius: 0.5rem; }
.thumb-img { position: absolute; top: 0; left: 0; width: 100%; height: 100%; object-fit: cover; }
/* ensure modal image fits viewport */
.modal img { max-height: 80vh; width: auto; }
</style>
