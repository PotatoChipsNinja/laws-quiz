<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >
      <div>
        <p class="text-h3" style="line-height: 120%">{{ textToShow }}</p>
      </div>

      <v-expand-transition>
        <v-card v-show="showQuestion" class="mx-2 mt-12 mb-2 pa-2" elevation="4" rounded="lg">
          <!-- <v-overlay
            opacity=".02"
            scrim="plain"
            contained
            model-value
            persistent
          /> -->
          <v-card-item>
            <v-card-title>QUIZ</v-card-title>
          </v-card-item>
          <v-card-text>
            <p class="text-h5">{{episode.question}}</p>
            <div class="py-2" />
            <v-row align="center" justify="center">
              <v-col v-for="(option, i) in episode.options" cols="auto">
                <v-btn
                  @click="choose(i)"
                  :color="hasChosen && i === chosenId ? (i === episode.answer ? 'success' : 'error') : (hasChosen && chosenId != episode.answer && i === episode.answer ? 'success' : 'plain')"
                >{{ option }}</v-btn>
              </v-col>
            </v-row>
          </v-card-text>
        </v-card>
      </v-expand-transition>

      <v-expand-transition>
        <div v-show="hasChosen">
          <v-card class="mx-2 mt-4 pa-2" :color="hasChosen && chosenId === episode.answer ? 'success' : 'error'" elevation="4" rounded="lg">
            <v-card-item>
              <v-card-title>{{ hasChosen && chosenId === episode.answer ? "回答正确" : "回答错误" }}</v-card-title>
            </v-card-item>
            <v-card-text>
              <p class="text-h6">{{ episode.analysis }}</p>
            </v-card-text>
          </v-card>

          <div class="text-center">
            <div class="py-4" />
            <v-btn size="x-large" @click="nextEpisode">{{ episode_id < quiz.episodes.length - 1 ? "继续故事" : "故事结束" }}</v-btn>
            <div class="py-1" />
          </div>
        </div>
      </v-expand-transition>

    </v-responsive>
  </v-container>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
// const { quizId, quizStatus } = defineProps(['quizId', 'quizStatus'])
const { quizId } = defineProps(['quizId'])
const emits = defineEmits(['update'])

import data from '@/assets/data.json'
import { h } from 'vue';
const quiz = computed(() => data[quizId])
const episode_id = ref(0)
const episode = computed(() => quiz.value.episodes[episode_id.value])
const text = computed(() => episode.value.text)
const textToShow = ref('')
const showQuestion = ref(false)
const hasChosen = ref(false)
const chosenId = ref(-1)

const typeWriter = () => {
  let i = 0
  const speed = 50 // 打字速度，单位为毫秒
  const textLength = text.value.length

  const typeInterval = setInterval(() => {
    textToShow.value += text.value[i]
    i++

    if (i === textLength) {
      showQuestion.value = true
      clearInterval(typeInterval)
    }
  }, speed)
}

const choose = (option) => {
  if (hasChosen.value) return
  hasChosen.value = true
  chosenId.value = option
  if (option === episode.value.answer) {
    console.log('回答正确')
  } else {
    console.log('回答错误')
  }
}

const nextEpisode = () => {
  console.log(episode_id.value, quiz.value.episodes.length)
  if (episode_id.value < quiz.value.episodes.length - 1) {
    showQuestion.value = false
    hasChosen.value = false
    chosenId.value = -1
    textToShow.value = ''
    episode_id.value++
    setTimeout(() => {
      typeWriter()
    }, 500)
  } else {
    emits('update', true, 0, 0)
  }
}

onMounted(() => {
  typeWriter()
})
</script>

<style>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
</style>
