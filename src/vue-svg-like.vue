<template>
  <svg
    class="like"
    :class="{clicked: clicked, disabled: disabled}"
    :width="svg.width"
    :height="svg.height"
    :viewBox="svg.viewBox"
    @click="onClickLikeButton"
  >
    <explosion
      class="explosion"
      :style="explosionStyle"
    />
    <g
      class="particleLayer"
      :style="particleStyle"
    >
      <particle
        v-for="particle in particles"
        :key="particle.id"
        :particle="particle"
        class="particle"
        :style="particleStyle"
      />
    </g>
    <heart
      class="heart"
      :style="heartStyle"
    />
  </svg>
</template>

<script>
import Explosion from './components/Explosion.vue'
import Particle from './components/Particle.vue'
import Heart from './components/Heart.vue'
import particles from './assets/particles.js'

const INIT_SVG = {
  width: 27.5,
  height: 25,
  viewBox: '0 0 500 500'
}

export default {
  name: 'vue-svg-like',
  components: {
    Explosion,
    Particle,
    Heart
  },
  props: {
    clicked: {
      type: Boolean,
      default: false
    },
    color: {
      type: String,
      default: '#f91880'
    },
    subColor: {
      type: String
    },
    size: {
      type: Number,
      default: 1
    },
    duration: {
      type: Number,
      default: 1
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      particles
    }
  },
  computed: {
    svg: function () {
      return {
        width: INIT_SVG.width * this.size,
        height: INIT_SVG.height * this.size,
        viewBox: INIT_SVG.viewBox
      }
    },
    heartStyle: function () {
      return {
        '--main-color': this.color,
        '--duration': this.duration + 's'
      }
    },
    explosionStyle: function () {
      return {
        '--sub-color': this.subColor || this.color,
        '--duration': this.duration + 's'
      }
    },
    particleStyle: function () {
      return {
        '--duration': this.duration + 's'
      }
    }
  },
  methods: {
    onClickLikeButton: function () {
      if (!this.disabled) {
        this.$emit('click')
      }
    }
  }
}
</script>

<style lang="scss">
@mixin center {
  transform-origin: 250px 250px;
}

$particleNum: 14;

.like {
  overflow: visible;
  cursor: pointer;
  .explosion {
    transform: scale(0.02);
    fill: none;
    opacity: 0;
    stroke: var(--sub-color);
    stroke-width: 1;
    @include center;
  }
  .particleLayer {
    transform: scale(3);
    opacity: 0;
    .particle {
      opacity: 0;
      @include center;
    }
  }
  .heart {
    fill: none;
    stroke: #9da8b3;
    stroke-width: 36px;
    @include center;
  }
  &:hover {
    .heart {
      stroke: var(--main-color);
    }
  }
  &.clicked {
    .explosion {
      animation: explosionAnime var(--duration) forwards;
    }
    .particleLayer {
      animation: particleLayerAnime var(--duration) forwards;

      @for $index from 1 through $particleNum {
        .particle:nth-child(#{$index}) {
          animation: particleAnimate#{$index} var(--duration) forwards;
        }
      }
    }
    .heart {
      fill: var(--main-color);
      stroke: var(--main-color);
      animation: heartAnime var(--duration) forwards;
    }
  }
  &.disabled {
    opacity: .25;
    cursor: default;
    .heart {
      stroke: #9da8b3;
    }
    &.clicked {
      .heart {
        stroke: var(--main-color);
      }
    }
  }
}

@keyframes explosionAnime {
  0% {
    opacity: 0;
    transform: scale(0.01);
  }
  1% {
    opacity: 1;
    transform: scale(0.01);
  }

  5% {
    stroke-width: 200;
  }

  20% {
    stroke-width: 300;
  }

  50% {
    opacity: .5;
    transform: scale(3);
    stroke-width: 1;
  }
  50.1% {
    stroke-width: 0;
  }

  100% {
    transform: scale(3);
    stroke-width: 0;
  }
}

@keyframes particleLayerAnime {
  0% {
    transform: translate(0, 0);
    opacity: 0;
  }
  30% {
    opacity: 0;
  }
  31% {
    opacity: 1;
  }

  60% {
    transform: translate(0, 0);
  }

  70% {
    opacity: 1;
  }

  100% {
    // opacity: 0;
    transform: translate(0, -50px);
  }
}

$points:
-48, -177,
123, 129,
150, -144,
-117, 108,
-117, 96,
144, 18,
-207, -108,
-36, -156,
-129, -63,
-30, 141,
198, -27,
120, -135,
87, 72,
-20, 150;

$pointer: 1;

@for $index from 1 through $particleNum {
  @keyframes particleAnimate#{$index} {
    0% {
      transform: translate(0, 0);
    }
    30% {
      opacity: 1;
      transform: translate(0, 0);
    }
    80% {
      transform: translate(#{nth($points, $pointer)}px, #{nth($points, $pointer + 1)}px);
    }
    90% {
      transform: translate(#{nth($points, $pointer)}px, #{nth($points, $pointer + 1)}px);
    }
    100% {
      opacity: 1;
      transform: translate(#{nth($points, $pointer)}px, #{nth($points, $pointer + 1)}px);
    }
  }
  $pointer: $pointer + 2;
}

@keyframes heartAnime {
  0% {
    transform: scale(0);
  }
  39% {
    transform: scale(0);
  }
  60% {
    transform: scale(1.2, 1.2);
  }
  70% {
    transform: scale(1, 1) translate(0%, -10%);
  }
  75% {
    transform: scale(1.1, 0.9) translate(0%, 5%);
  }
  80% {
    transform: scale(0.95, 1.05) translate(0%, -3%);
  }
  100% {
    transform: scale(1.0, 1.0) translate(0%, 0%);
  }
}
</style>
