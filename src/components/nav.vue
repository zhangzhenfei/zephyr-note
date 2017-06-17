<script type="text/javascript">
import light from '!raw-loader!muse-ui/dist/theme-default.css'
import dark from '!raw-loader!muse-ui/dist/theme-dark.css'
import carbon from '!raw-loader!muse-ui/dist/theme-carbon.css'
import teal from '!raw-loader!muse-ui/dist/theme-teal.css'

export default {
  data() {
    return {
      theme: 'carbon',
      isCategorgShow: true,
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
    mainButtonClick() {
      this.$emit('mainButtonClick')
    }
  }
}
</script>

<template>
  <mu-appbar title="和风笔记">
    <mu-icon-button icon="menu" slot="left" @click="mainButtonClick" />
    <mu-icon-menu icon="palette" slot="right" tooltip="主题" :value="theme" @change="changeTheme">
      <mu-menu-item title="light" value="light" />
      <mu-menu-item title="dark" value="dark" />
      <mu-menu-item title="carbon" value="carbon" />
      <mu-menu-item title="teal" value="teal" />
    </mu-icon-menu>
  </mu-appbar>
</template>
