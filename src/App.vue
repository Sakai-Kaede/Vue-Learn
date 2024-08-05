<script setup>
import { ref, reactive, computed, watch, watchEffect } from 'vue'
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
const courseInfo = {
  sections: ref(10),
  language: ref('Japanese')
}
console.log(courseInfo.sections.value)

// ------ 以下templateについて ------ //
const count = ref(2)
const message = ref('<h1>Hello</h1>')
const vueURL = ref('https://vuejs.org')
const vueId = ref('vue-link')
const count1 = ref(0)
const count2 = ref(0)
const count3 = ref(0)
const eventName = 'keyup'
const userInput = ref('')
const score = ref(0)
// computedは処理をまとめるためのもの
// リアクティブなデータの変化を監視し、更新できる
// 監視されている値に変化があった場合、関数が再度実行される(常に実行されるわけではない)
const evaluation = computed(() => {
  return score.value > 3 ? '4以上です' : '3以下です'
})
const count4 = ref(0)
watchEffect(() => {
  console.log(count4.value)
  setTimeout(() => {
    'after 1 second'
  }, 1000)
  count4.value = 'hello'
})
</script>

<template>
  <h1>Title: {{ title }}</h1>
  <!-- template内では、refオブジェクトにvalueが加えられる -->
  <h2>Price: ${{ price - 1 }}</h2>
  <button @click="increment">button</button>
  <!-- Vueはデータの先頭で判断する(この場合はcourseInfo) -->
  <!-- データの先頭がただのオブジェクトであるため、.valueが必要 -->
  <h2>Course Info Sections: {{ courseInfo.sections.value }}</h2>

  <!-- ------ 以下templateについて ------ -->
  <div>{{ count + 3 }}</div>
  <!-- 二重波括弧の中は単一の式のみ定義できる -->
  <div>{{ count > 3 ? 'Yes' : 'No' }}</div>
  <!-- v-htmlはセキュリティ上の問題がある。
  特に、ユーザから受け取った値を表示する場合は注意 -->
  <div v-html="message"></div>
  <!-- 属性値には、v-bindを使う。省略記法は「:」 -->
  <a :href="vueURL">Vue.js</a>
  <!-- 複数の属性にv-bindを付加する -->
  <a v-bind="{ id: vueId, href: vueURL }">Vue.js</a>
  <p>{{ count1 }}</p>
  <!-- イベント修飾子で親イベントへの伝播を止める -->
  <div @click="count1++">
    <button @click.stop="count1 = 30">button</button>
  </div>
  {{ count2 }}
  <input type="text" @keyup.space="count2++" />
  <!-- v-on（名前）:click（引数）.prevent（修飾子）='changeData（値）' -->
  <br />
  {{ count3 }}
  <!-- 角括弧([])を使って引数にデータを指定する -->
  <input type="text" @[eventName].space.delete="count3++" />
  <br />
  <p>{{ userInput }}</p>
  <!-- ユーザーが入力した値をscriptで受け取る -->
  <input v-model="userInput" type="text" />
  <p>{{ score }}</p>
  <p>{{ evaluation }}</p>
  <button @click="score++">+1</button>
  <p>{{ count4 }}</p>
  <button @click="count4++">+1</button>
</template>

<style>
h1 {
  color: red;
}
</style>
