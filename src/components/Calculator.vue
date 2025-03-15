<script setup lang="ts">
import { ref, onMounted } from 'vue'

const display = ref('');
const history = ref<{ id: number; expression: string; result: string }[]>([]);

// 数字や演算子が押された時の処理
const handleClick = (value: string) => {
  display.value += value;
};

// 計算関数
const calculate = async () => {
  try {
    const result = eval(display.value).toString();

    // 結果をサーバに保存
    await fetch('http://localhost:3000/calculations', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ expression: display.value, result }),
    });

    display.value = result;
    fetchHistory();
  } catch (e) {
    display.value = '計算失敗';
  }
};

// モックサーバから履歴を取得
const fetchHistory = async () => {
  const res = await fetch('http://localhost:3000/calculations');
  history.value = await res.json();
};

// 初回読み込み時に履歴を取得
onMounted(fetchHistory);
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
      <button @click="display = ''">C</button>
      <button @click="handleClick('/')">/</button>
    </div>

    <h2>履歴</h2>
    <ul>
      <li v-for="item in history" :key="item.id">
        {{ item.expression }} = {{ item.result }}
      </li>
    </ul>
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
