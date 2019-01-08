<template>
  <div>
    <div class="canvases" :style="style">
      <canvas v-bind="{width, height}" ref="drawer" ></canvas>
      <canvas-drawer v-bind="{width, height, penWidth, before}" ref="drawer" />
      <canvas-cursor v-bind="{width, height, penWidth}" ref="cursor" />
      <div :style="style"
        @mousemove="move($event.offsetX, $event.offsetY)" @touchmove="touchmove"
        @mousedown="down($event.offsetX, $event.offsetY)" @touchstart="touchstart"
        @mouseup="up"     @touchend="up"
       ></div>
    </div>
    <input type="range" v-model="penWidth">
  </div>
</template>
<script>
import CanvasCursor from "./MainCanvasCursor.vue";
import CanvasDrawer from "./MainCanvasDrawer.vue";

const getOffsetFromTouch = touch => {
  //abs
  const rect = touch.target.getBoundingClientRect();
  return {
    x: touch.clientX - rect.x,
    y: touch.clientY - rect.y
  };
  return rect;
};
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
    move(x, y) {
      if (this.before) this.draw(x, y);
      this.$refs.cursor.drawCursor(x, y);
    },
    down(x, y) {
      this.$set(this, "before", { x, y });
    },
    up() {
      this.before = null;
    },
    touchstart(e) {
      const touch = e.changedTouches[0];
      const { x, y } = getOffsetFromTouch(touch);
      this.down(x, y);
    },
    touchmove(e) {
      const touch = e.changedTouches[0];
      const { x, y } = getOffsetFromTouch(touch);
      this.move(x, y);
    },
    mousedown(e) {
      this.down(e.offsetX, e.offsetY);
    },
    draw(x, y) {
      this.$refs.drawer.draw(x, y);
      this.before = { x, y };
    }
  },
  data() {
    return {
      width: 500,
      height: 600,
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
