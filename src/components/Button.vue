<template>
  <button @click="setState">
    <Icon :iconName="iconName" />
  </button>
</template>

<script>
import Icon from './Icon.vue'

export default {
  name: 'Button',
  props: {
    iconName: String,
    active: Boolean,
  },
  components: {
    Icon,
  },
  methods: {
    setState() {
      this.$emit('setState')
    },
  },
}
</script>

<style></style>
