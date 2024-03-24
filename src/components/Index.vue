<template>
  <v-container class="fill-height">
    <v-responsive
      class="align-centerfill-height mx-auto"
      max-width="900"
    >
      <v-row class="justify-center">
        <v-col cols="2" class="align-self-center">
          <v-img
            class="ml-4"
            src="@/assets/ict_logo.png"
          />
        </v-col>
        <v-divider vertical class="px-3"></v-divider>
        <v-col cols="2" class="align-self-center">
          <span>研究生会LOGO</span>
          <!-- <v-img
            class="mr-4"
            src="@/assets/logo.png"
          /> -->
        </v-col>
      </v-row>

      <div class="py-4" />

      <div class="text-center">
        <h1 class="text-h2 font-weight-bold">普法情景互动答题</h1>
      </div>

      <div class="py-4" />

      <div class="text-center">
        <p class="text-h5 font-weight-light">根据情景描述及提示进行选择，回答正确到故事结束即可获得盖章</p>
      </div>

      <div class="py-4" />

      <v-row>
        <v-col cols="6">
          <v-card
            class="py-4 menu-card"
            color="surface-variant"
            prepend-icon="mdi-text-box-outline"
            rel="noopener noreferrer"
            rounded="lg"
            subtitle="扮演公司员工李华完成维权"
            target="_blank"
            title="劳动合同法"
            variant="text"
            @click="enter(0)"
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

        <v-col cols="6">
          <v-card
            class="py-4 menu-card"
            color="surface-variant"
            prepend-icon="mdi-star-circle-outline"
            rel="noopener noreferrer"
            rounded="lg"
            subtitle="TBD"
            target="_blank"
            title="TBD"
            variant="text"
            @click="enter(1)"
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

        <v-col cols="6">
          <v-card
            class="py-4 menu-card"
            color="surface-variant"
            prepend-icon="mdi-widgets-outline"
            rel="noopener noreferrer"
            rounded="lg"
            subtitle="TBD"
            target="_blank"
            title="TBD"
            variant="text"
            @click="enter(2)"
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

        <v-col cols="6">
          <v-card
            class="py-4 menu-card"
            color="surface-variant"
            prepend-icon="mdi-account-group-outline"
            rel="noopener noreferrer"
            rounded="lg"
            subtitle="TBD"
            target="_blank"
            title="TBD"
            variant="text"
            @click="enter(3)"
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
    </v-responsive>
  </v-container>
</template>

<script setup>
const emits = defineEmits(['update'])

function enter (quizId) {
  emits('update', false, quizId, 0)
}
</script>

<style>
  .menu-card i {
    margin-right: 10px;
  }
</style>
