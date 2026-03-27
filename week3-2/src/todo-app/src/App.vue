<script setup>
import { ref } from 'vue'

const buttonName = ref('버튼123')

function test() {
  alert('haha')
}

console.log(buttonName.value)

globalThis.test = buttonName
</script>

<template>
  <h1>You did it!</h1>
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>

  <div>
    <Button @click="test">{{ buttonName }}</Button> <br />
    <InputText placeholder="Username" v-model="buttonName" /> <br />
    <input type="text" placeholder="Username" :value="버튼12333" />
  </div>
</template>

<style scoped></style>
