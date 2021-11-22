<script setup>
import { ref } from 'vue';
let isGameOver = false; // 游戏是否结束
let whichOne = 'white'; // 一开始是白色的棋子
const chessArr = ref([]);
const board = ref(null);

function handleClick(e, row, col) {
  console.log(row, col);
  console.log(e.offsetX, e.offsetY);

  let tdw = (board.value.clientWidth * 0.93) / 14;

  let positionX = e.offsetX > tdw / 2;
  let positionY = e.offsetY > tdw / 2;

  let chessPoint = {
    x: positionX ? parseInt(col) : parseInt(col) - 1,
    y: positionY ? parseInt(row) : parseInt(row) - 1,
    c: whichOne,
  };

  chessArr.push(chessPoint);

  whichOne = whichOne === 'white' ? 'black' : 'white'; // 切换棋子的颜色
}
</script>

<template lang="">
    <div class="container">
        <table class="chessboard" ref="board">
            <tr v-for="iRow in 14" :key="iRow">
                <td v-for="iCol in 14" :key="iCol" @click="handleClick($event, iRow, iCol)">
                  <div class="chess black"></div>
                </td>
            
            </tr>
        </table>
    </div>
</template>


<style >
.container {
  border: 1px solid rgb(207, 188, 188);
  width: 500px;
  height: 500px;
  margin: 50px auto;
  /* 是一个弹性盒子，我们这边的设置代表让里面的内容水平垂直居中 */
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgb(247, 230, 183);
}

/* 棋盘里面的格子的样式 */
.chessboard {
  width: 92%;
  height: 92%;
  /* 设置表格的行列之间没有间隙 */
  border-collapse: collapse;
}

.chessboard td {
  border: 1px solid black;
  position: relative;
}

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