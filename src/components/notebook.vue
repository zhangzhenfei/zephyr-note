<script>
export default {
  props:
  {
    isShowNotebook: {
      type: Boolean,
      default: true,
      required: true
    },
    isFixedNotebook: {
      type: Boolean,
      default: true,
      required: true
    }
  }
}
</script>

<template>
  <mu-drawer :open="isShowNotebook" :docked="isFixedNotebook">
    <mu-list>
      <mu-list-item title="Menu Item 1" />
      <mu-list-item title="Menu Item 2" />
      <mu-list-item title="Menu Item 3" />
    </mu-list>
  </mu-drawer>
</template>

<style lang="scss">
.mu-drawer {
  margin-top: 64px;
  background-color: #F8F8F8;
}
</style>
