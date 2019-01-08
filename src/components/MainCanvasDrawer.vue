<template>
  <canvas 
    :width="width" :height="height" ref="canvas"
    ></canvas>
</template>
<script>
export default {
  props: ["width", "height", "penWidth", "before"],
  computed: {
    context() {
      return this.$refs.canvas.getContext("2d");
    }
  },
  methods: {
    draw(x, y) {
      const ctx = this.context;
      ctx.beginPath();
      // ctx.globalAlpha = defoalpha;
      //継続値が初期値の場合は、現在のマウス位置をスタート位置とする
      ctx.moveTo(this.before.x, this.before.y);
      //lineTo（ゴール地点）の決定、現在のマウス位置をゴール地点とする
      ctx.lineTo(x, y);
      //直線の角を「丸」、サイズと色を決める
      ctx.lineCap = "round";
      ctx.lineWidth = this.penWidth;
      ctx.strokeStyle = "#555555";
      ctx.stroke();
    }
  }
};
</script>
