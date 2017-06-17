<script type="text/javascript">
import light from '!raw-loader!muse-ui/dist/theme-default.css'
import dark from '!raw-loader!muse-ui/dist/theme-dark.css'
import carbon from '!raw-loader!muse-ui/dist/theme-carbon.css'
import teal from '!raw-loader!muse-ui/dist/theme-teal.css'

import Nav from '@/components/nav'
import Notebook from '@/components/notebook'
import NoteContent from '@/components/note-content'

export default {
  data() {
    return {
      isShowNotebook: true,
      isFixedNotebook: true,
      contentIsFullWidth: false,
      theme: 'light',
      themes: {
        light,
        dark,
        carbon,
        teal
      }
    }
  },
  methods: {
    changeTheme(theme) {
      this.theme = theme
      const styleEl = this.getThemeStyle()
      styleEl.innerHTML = this.themes[theme] || ''
    },
    getThemeStyle() {
      const themeId = 'muse-theme'
      let styleEl = document.getElementById(themeId)
      if (styleEl) { return styleEl }
      styleEl = document.createElement('style')
      styleEl.id = themeId
      document.body.appendChild(styleEl)
      return styleEl
    },
    navMainButtonClickEvent() {
      this.isShowNotebook = !this.isShowNotebook
      this.contentIsFullWidth = !this.contentIsFullWidth
    }
  },
  components: {
    'note-nav': Nav,
    'notebook': Notebook,
    'note-content': NoteContent
  }
}

</script>

<template>
  <div class="container">
    <note-nav @mainButtonClick="navMainButtonClickEvent" />
    <notebook :isShowNotebook="isShowNotebook" :isFixedNotebook="isFixedNotebook" />
    <note-content :isFullWidth="contentIsFullWidth" />
  </div>
</template>

<style lang="scss" scoped>
.container {
  width: 100%;
  height: 100%;
}
</style>
