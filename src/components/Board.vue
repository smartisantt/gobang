<script setup>
import { ref, computed } from "vue";
import Chess from "./Chess.vue";
let isGameOver = false; // 游戏是否结束
let whichOne = "white"; // 一开始是白色的棋子
const chessArrRef = ref([]);
const boardRef = ref(null);

function exist(chessPoint) {
  let result = chessArrRef.value.find((item) => {
    return item.x === chessPoint.x && item.y === chessPoint.y;
  });
  return result === undefined ? true : false;
}

function handleClick(e, row, col) {
  if (isGameOver) {
    if (window.confirm("是否要重新开始一局？")) {
      chessArrRef.value = []; // 重置棋子的数组
      isGameOver = false;
    }
    return;
  }
  let tdw = (boardRef.value.clientWidth * 0.92) / 14;

  let positionX = e.offsetX > tdw / 2;
  let positionY = e.offsetY > tdw / 2;

  let chessPoint = {
    x: positionX ? parseInt(col) + 1 : parseInt(col),
    y: positionY ? parseInt(row) + 1 : parseInt(row),
    c: whichOne,
  };

  if (exist(chessPoint) && !isGameOver) {
    chessArrRef.value.push(chessPoint);
    check();
    whichOne = whichOne === "white" ? "black" : "white"; // 切换棋子的颜色
  }
}

// 检查游戏是否结束，检查是否有符合要求的棋子
function check() {
  // 其实就是遍历数组里面的每一个棋子
  // 这里分为 4 种情况：横着、竖着、斜着（2 种）

  for (let i = 0; i < chessArrRef.value.length; i++) {
    let curChess = chessArrRef.value[i];
    let chess2, chess3, chess4, chess5;

    // 检查有没有横着的 5 个颜色一样的棋子
    chess2 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 1 &&
        curChess.y === item.y &&
        curChess.c === item.c
      );
    });
    chess3 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 2 &&
        curChess.y === item.y &&
        curChess.c === item.c
      );
    });
    chess4 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 3 &&
        curChess.y === item.y &&
        curChess.c === item.c
      );
    });
    chess5 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 4 &&
        curChess.y === item.y &&
        curChess.c === item.c
      );
    });
    if (chess2 && chess3 && chess4 && chess5) {
      // 进入此 if，说明游戏结束
      end(curChess, chess2, chess3, chess4, chess5);
    }

    // 检查有没有竖着的 5 个颜色一样的棋子
    chess2 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x &&
        curChess.y === item.y + 1 &&
        curChess.c === item.c
      );
    });
    chess3 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x &&
        curChess.y === item.y + 2 &&
        curChess.c === item.c
      );
    });
    chess4 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x &&
        curChess.y === item.y + 3 &&
        curChess.c === item.c
      );
    });
    chess5 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x &&
        curChess.y === item.y + 4 &&
        curChess.c === item.c
      );
    });
    if (chess2 && chess3 && chess4 && chess5) {
      // 进入此 if，说明游戏结束
      end(curChess, chess2, chess3, chess4, chess5);
    }

    // 检查有没有斜着的 5 个颜色一样的棋子
    chess2 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 1 &&
        curChess.y === item.y + 1 &&
        curChess.c === item.c
      );
    });
    chess3 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 2 &&
        curChess.y === item.y + 2 &&
        curChess.c === item.c
      );
    });
    chess4 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 3 &&
        curChess.y === item.y + 3 &&
        curChess.c === item.c
      );
    });
    chess5 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x + 4 &&
        curChess.y === item.y + 4 &&
        curChess.c === item.c
      );
    });
    if (chess2 && chess3 && chess4 && chess5) {
      // 进入此 if，说明游戏结束
      end(curChess, chess2, chess3, chess4, chess5);
    }

    // 检查有没有斜着的 5 个颜色一样的棋子
    chess2 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x - 1 &&
        curChess.y === item.y + 1 &&
        curChess.c === item.c
      );
    });
    chess3 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x - 2 &&
        curChess.y === item.y + 2 &&
        curChess.c === item.c
      );
    });
    chess4 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x - 3 &&
        curChess.y === item.y + 3 &&
        curChess.c === item.c
      );
    });
    chess5 = chessArrRef.value.find(function (item) {
      return (
        curChess.x === item.x - 4 &&
        curChess.y === item.y + 4 &&
        curChess.c === item.c
      );
    });
    if (chess2 && chess3 && chess4 && chess5) {
      end(curChess, chess2, chess3, chess4, chess5);
    }
  }
}

function end() {
  if (!isGameOver) {
    isGameOver = true;

    // 2. 把获胜的棋子加上一个红色阴影
    for (let i = 0; i < arguments.length; i++) {
      arguments[i].win = "win";
    }
  }
}
</script>

<template lang="">
  <div class="container">
    <table class="chessboard" ref="boardRef">
      <tr v-for="y in 14" :key="y">
        <td
          v-for="x in 14"
          :key="x"
          @click="handleClick($event, y, x)"
        >
          
          <Chess v-if="x===14" :point="{x:15,y}" :chessArr="chessArrRef" :style="{left:'50%'}" />
          <Chess v-if="y===14" :point="{x,y:15}" :chessArr="chessArrRef" :style="{top:'50%'}" />
          <Chess v-if="x===14 && y===14" :point="{x:15,y:15}" :chessArr="chessArrRef" :style="{left:'50%',top:'50%'}" />
          <Chess :point="{x,y}" :chessArr="chessArrRef" />
        </td>
      </tr>
    </table>
  </div>
</template>

<style>
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
</style>
