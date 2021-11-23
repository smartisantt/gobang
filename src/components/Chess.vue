<script setup>
import { computed } from "vue";
const props = defineProps({
  point: Object,
  chessArr: Array,
});

const chess = computed(() =>
  props.chessArr.find((it) => {
    return it.x == props.point.x && it.y == props.point.y;
  })
);
</script>

<template>
  <div
    v-if="chess"
    :class="{
      chess: Boolean(chess),
      white: chess.c === 'white',
      black: chess.c === 'black',
      win: chess.win === 'win',
    }"
    @click.stop
  ></div>
</template>

 

<style>
/* 棋子的公共样式 */
.chess {
  border: 1px solid lightgrey;
  border-radius: 50%;
  position: absolute;
  left: -50%;
  top: -50%;
  width: 90%;
  height: 90%;
  color: lightgrey;
  font-size: 12px;
  font-weight: bold;
  /* 让文字居中 */
  display: flex;
  justify-content: center;
  align-items: center;
}

/* 白色棋子 */
.white {
  background-color: #fff;
}

/* 黑色棋子 */
.black {
  background-color: #000;
}

/* 获胜棋子 */
.win {
  border: 1px solid red;
  box-shadow: 0 0 3px 2px red; /* 红色阴影 */
}
</style>