<template>
  <v-app>
    <v-main>
      <Index v-if="atIndex" :atIndex="atIndex" @update="update" />
      <Quiz v-if="!atIndex" :quizId="quizId" @update="update" />
    </v-main>

    <AppFooter />
  </v-app>
</template>

<script setup>
import { ref } from 'vue'

const atIndex = ref(true)
const quizId = ref(-1)

const update = (newAtIndex, newQuizId) => {
  atIndex.value = newAtIndex
  quizId.value = newQuizId
}
</script>
