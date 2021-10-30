<template>
  <circle
    :fill="particle.fill"
    :cx="particle.cx"
    :cy="particle.cy"
    :r="particle.r"
  />
</template>

<script>
export default {
  name: 'particlej',
  props: {
    particle: {
      type: Object,
      required: true
    }
  }
}
</script>
