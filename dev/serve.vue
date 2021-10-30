<script>
import Vue from 'vue';
import VueSvgLike from '@/vue-svg-like.vue';

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueSvgLike
  }
});
</script>

<template>
  <div id="app">
    <vue-svg-like />
  </div>
</template>
