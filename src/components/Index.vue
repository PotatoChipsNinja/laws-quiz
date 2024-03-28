<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >
      <v-row class="justify-center px-15">
        <v-col cols="3" class="align-self-center mx-6">
          <v-img
            src="@/assets/ict_logo.png"
          />
        </v-col>
        <v-divider vertical></v-divider>
        <v-col cols="3" class="align-self-center mx-6">
          <!-- <span>研究生会LOGO</span> -->
          <v-img
            v-if="theme.global.current.value.dark"
            src="@/assets/su_logo_dark.png"
          />
          <v-img
            v-if="!theme.global.current.value.dark"
            src="@/assets/su_logo.png"
          />
        </v-col>
      </v-row>

      <div class="py-6" />

      <div class="text-center">
        <h1 class="text-h2 font-weight-bold">普法情景互动答题</h1>
      </div>

      <div class="py-4" />

      <div class="text-center">
        <p class="text-h5 font-weight-light">根据情景描述及提示进行选择，完成任意故事即可获得盖章</p>
      </div>

      <div class="py-6" />

      <v-row v-if="!randomMode">
        <v-col cols="6" v-for="(item, i) in data">
          <v-card
            class="py-1 menu-card"
            color="surface-variant"
            :prepend-icon="item.icon"
            rel="noopener noreferrer"
            rounded="lg"
            :subtitle="item.description"
            target="_blank"
            :title="item.topic"
            variant="text"
            @click="enter(i)"
          >
            <v-overlay
              opacity=".06"
              scrim="primary"
              contained
              model-value
              persistent
            />
          </v-card>
        </v-col>
      </v-row>

      <v-row v-if="randomMode" class="text-center align-centerfill-height mx-auto">
        <v-col class="pb-5">
          <v-btn prepend-icon="mdi-dice-5" color="primary" size="x-large" @click="randomQuiz">开始随机情景</v-btn>
        </v-col>
      </v-row>
    </v-responsive>
  </v-container>
</template>

<script setup>
import { useTheme } from 'vuetify'
import data from '@/assets/data.json'

const theme = useTheme()
const { randomMode } = defineProps(['randomMode'])
const emits = defineEmits(['update'])

const enter = (quizId) => {
  emits('update', false, quizId)
}

const randomQuiz = () => {
  const quizId = Math.floor(Math.random() * data.length)
  emits('update', false, quizId)
}
</script>

<style>
.menu-card i {
  margin-right: 10px;
}
</style>
