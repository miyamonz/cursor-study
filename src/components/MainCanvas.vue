<template>
  <div>
  <div class="canvases" :style="style">
    <canvas v-bind="{width, height}" ref="drawer" ></canvas>
    <canvas-drawer v-bind="{width, height, penWidth, before}" ref="drawer" />
    <canvas-cursor v-bind="{width, height, penWidth}" ref="cursor" />
    <div :style="style"
      @mousemove="mousemove"
      @mousedown="mousedown"
      @mouseup="mouseup"
     ></div>
  </div>
  <input type="range" v-model="penWidth">
  </div>
</template>
<script>
import CanvasCursor from "./MainCanvasCursor.vue";
import CanvasDrawer from "./MainCanvasDrawer.vue";
export default {
  components: { CanvasCursor, CanvasDrawer },
  mounted() {},
  computed: {
    style() {
      return {
        width: this.width + "px",
        height: this.height + "px"
      };
    }
  },
  methods: {
    mousemove(e) {
      const { offsetX: x, offsetY: y } = e;
      if (this.before) this.draw(x, y);
      this.$refs.cursor.drawCursor(x, y);
    },
    mousedown(e) {
      this.$set(this, "before", { x: e.offsetX, y: e.offsetY });
    },
    mouseup() {
      this.before = null;
    },
    draw(x, y) {
      this.$refs.drawer.draw(x, y);
      this.before = { x, y };
    }
  },
  data() {
    return {
      width: 400,
      height: 500,
      penWidth: 5,
      before: null
    };
  }
};
</script>
<style>
.canvases {
  position: relative;
  margin: 0 auto;
  border: solid 1px;
}
.canvases > * {
  position: absolute;
  top: 0;
  left: 0;
}
</style>
