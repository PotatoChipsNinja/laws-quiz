<template>
  <v-footer height="40" app>
    <div
      class="text-caption text-disabled"
    >
      <a
        class="d-inline-block mx-2 social-link"
        rel="noopener noreferrer"
        target="_blank"
        @click="toggleTheme"
      >
        <v-icon
          icon="mdi-theme-light-dark"
          size="16"
        />
      </a>
      <a
        class="d-inline-block mx-2 social-link"
        rel="noopener noreferrer"
        target="_blank"
        @click="reload"
      >
        <v-icon
          icon="mdi-reload"
          size="16"
        />
      </a>
      <a
        class="d-inline-block mx-2 social-link"
        rel="noopener noreferrer"
        target="_blank"
        @click="switchMode"
      >
        <v-icon
          icon="mdi-dice-multiple"
          size="16"
        />
      </a>
      {{ (new Date()).toLocaleString() }}
    </div>

    

    <div
      class="text-caption text-disabled"
      style="position: absolute; right: 16px;"
    >
      &copy; 2024 <span class="d-none d-sm-inline-block">中国科学院计算技术研究所研究生会</span>
    </div>
  </v-footer>
</template>

<script setup>
import { useTheme } from 'vuetify'

const theme = useTheme()
const emits = defineEmits(['switchMode'])

const toggleTheme = () => {
  theme.global.name.value = theme.global.current.value.dark ? 'light' : 'dark'
}

const reload = () => {
  window.location.reload()
}

const switchMode = () => {
  emits('switchMode')
}
</script>

<style scoped lang="sass">
  .social-link :deep(.v-icon)
    color: rgba(var(--v-theme-on-background), var(--v-disabled-opacity))
    text-decoration: none
    transition: .2s ease-in-out

    &:hover
      color: rgba(25, 118, 210, 1)
</style>

