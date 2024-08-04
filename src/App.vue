<script setup>
import { ref, reactive } from 'vue'
const title = ref('Vue.js Course')
let price = ref(9.99)
function increment() {
  price.value = price.value + 1
}
const instructor = reactive({
  name: 'Kaede',
  age: 25,
  email: ref('kaede@example.com')
})
console.log(instructor.age)
// reactiveオブジェクト内のref要素に
// アクセス時.valueを省略する必要がある
// ただし、配列の要素の場合は.valueが必要である
console.log(instructor.email)
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <!-- template内では、refオブジェクトにvalueが加えられる -->
  <h2>Price: ${{ price - 1 }}</h2>
  <button @click="increment">button</button>
  <h2>Students: {{ info.students }}</h2>
</template>

<style>
h1 {
  color: red;
}
</style>
