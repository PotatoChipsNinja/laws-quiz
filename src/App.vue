<template>
  <v-app>
    <v-main>
      <Index v-if="atIndex" :atIndex="atIndex" :randomMode="randomMode" @update="update" />
      <Quiz v-if="!atIndex" :quizId="quizId" @update="update" />
    </v-main>

    <AppFooter @switchMode="switchMode" />
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const atIndex = ref(true)
const quizId = ref(-1)
const randomMode = ref(false)

const update = (newAtIndex, newQuizId) => {
  atIndex.value = newAtIndex
  quizId.value = newQuizId
}

const switchMode = () => {
  randomMode.value = !randomMode.value
}
</script>
