<script setup lang="ts">
import { ref } from 'vue';

// 表示用変数(リアクティブ)
const display = ref('');

// 数字や演算子が押された時の処理
const handleClick = (value: string) => {
  display.value += value;
};

// 計算関数
const calculate = () => {
  // 計算失敗を網羅的にキャッチ
  try {
    display.value = eval(display.value).toString(); // evalで計算
  } catch (e) {
    display.value = '計算失敗';
  }
};

// クリア関数
const clear = () => {
  display.value = '';
};
</script>

<template>
  <div>
    <h1>電卓</h1>
    <input type="text" v-model="display" disabled />
    <div>
      <button @click="handleClick('1')">1</button>
      <button @click="handleClick('2')">2</button>
      <button @click="handleClick('3')">3</button>
      <button @click="handleClick('+')">+</button>
    </div>
    <div>
      <button @click="handleClick('4')">4</button>
      <button @click="handleClick('5')">5</button>
      <button @click="handleClick('6')">6</button>
      <button @click="handleClick('-')">-</button>
    </div>
    <div>
      <button @click="handleClick('7')">7</button>
      <button @click="handleClick('8')">8</button>
      <button @click="handleClick('9')">9</button>
      <button @click="handleClick('*')">*</button>
    </div>
    <div>
      <button @click="handleClick('0')">0</button>
      <button @click="calculate">=</button>
      <button @click="clear">C</button>
      <button @click="handleClick('/')">/</button>
    </div>
  </div>
</template>

<style scoped>
button {
  font-size: 20px;
  width: 50px;
  height: 50px;
  margin: 5px;
}
</style>
