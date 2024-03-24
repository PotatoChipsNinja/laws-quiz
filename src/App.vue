<template>
  <v-app>
    <v-main>
      <Index v-if="atIndex" :atIndex="atIndex" @update="update" />
      <Quiz v-if="!atIndex" :quizId="quizId" :quizStatus="quizStatus" @update="update" />
    </v-main>

    <AppFooter />
  </v-app>
</template>

<script setup>
import { ref } from 'vue'
const atIndex = ref(true)
const quizId = ref(0)
const quizStatus = ref(0)

function update (newAtIndex, newQuizId, newQuizStatus) {
  atIndex.value = newAtIndex
  quizId.value = newQuizId
  quizStatus.value = newQuizStatus
}
</script>
