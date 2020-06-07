<template>
  <div class="w-full h-full inline-block bc-container" @click="$emit('click')">
    <svg
      v-bind="$attrs"
      :viewBox="viewBox"
      width="100%"
      height="100%"
      style="overflow:visible"
      class="bc-svg"
      :fill="color"
      ref="svg"
    >
      <path stroke-width="0" :d="`m0,0${d}`"></path>
      <text
        class="bc-text"
        :dx="dx"
        :dy="dy"
        :fill="textColor"
        ref="svgText"
      >{{text}}</text>
    </svg>
  </div>
</template>
<script>
function mounted() {
  this.computedText();
  this.computedD();
}

function computedText() {
  const { svgText: { textLength: { baseVal: { value } } } } = this.$refs;
  this.textWidth = value + 24;
}

function computedD() {
  const w = this.textWidth;
  const { svg: { clientHeight: h } } = this.$refs;
  this.viewBox = `0 0 ${w} ${h}`;
  const ratioX = h * (4 / 10);
  this.d = `
    h${w}l${ratioX},${h / 2}l-${ratioX},${h / 2}h-${w}l${ratioX},-${h / 2}l-${ratioX},-${h / 2}
  `;
  this.dx = ratioX + 6;
  this.dy = h / 2 + 5;
  this.updateSvgWidthHeight(w, h);
}

function updateSvgWidthHeight(w, h) {
  this.$refs.svg.setAttribute('width', w);
  this.$refs.svg.setAttribute('height', h);
}

function data() {
  return {
    d: '',
    dx: 0,
    dy: 0,
    textWidth: '',
    viewBox: '0 0 100 100',
  };
}

export default {
  name: 'bread-crumbs-dl',
  data,
  inheritAttrs: false,
  methods: {
    computedD,
    computedText,
    updateSvgWidthHeight,
  },
  mounted,
  props: {
    color: {
      default: 'currentColor',
      type: String,
    },
    text: {
      default: '',
      type: String,
    },
    textColor: {
      default: 'white',
      type: String,
    },
  },
};
</script>
