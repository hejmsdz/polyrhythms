<template>
  <svg :width="size" :height="size">
    <circle class="face" :cx="radius" :cy="radius" :r="radius" />

    <g v-for="circle in circles">
      <circle class="circle" :cx="radius" :cy="radius" :r="circle.radius" />
      <circle v-for="dot in circle.dots" class="dot" :cx="dot.x" :cy="dot.y" r="10" />
    </g>
  </svg>
</template>

<script>
const dotsCoordinates = (r, cx, cy, count) => {
  const coordinates = [];
  for (let i = 0; i < count; i++) {
    const angle = 2 * Math.PI * (i / count - 0.25);
    const x = cx + r * Math.cos(angle);
    const y = cy + r * Math.sin(angle);
    coordinates.push({ x, y });
  }
  return coordinates;
};

export default {
  name: 'clock',
  props: {
    size: Number,
    subdivisions: Array
  },
  computed: {
    radius: function() {
      return this.size / 2;
    },
    circles: function() {
      return this.subdivisions.map((count, i) => {
        const circleRadius = this.radius * (i + 1) / (this.subdivisions.length + 1);
        const dots = dotsCoordinates(circleRadius, this.radius, this.radius, count);
        return { radius: circleRadius, dots };
      });
    }
  }
}
</script>

<style>
.face {
  fill: #222;
}

.circle {
  stroke: #ddd;
  fill: transparent;
}

.dot {
  fill: #ddd;
}
</style>
