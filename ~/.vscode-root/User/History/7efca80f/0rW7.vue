<!-- eslint-disable vue/multi-word-component-names -->

<script setup lang="ts"></script>

<template>
  <div>
    <h1>電卓</h1>
    <input type="text" disabled />
    <div>
      <button>1</button>
      <button>2</button>
      <button>3</button>
      <button>+</button>
    </div>
    <div>
      <button>4</button>
      <button>5</button>
      <button>6</button>
      <button>-</button>
    </div>
    <div>
      <button>7</button>
      <button>8</button>
      <button>9</button>
      <button>*</button>
    </div>
    <div>
      <button>0</button>
      <button>=</button>
      <button>C</button>
      <button>/</button>
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
