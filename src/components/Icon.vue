<template>
  <div @click="onClick" class="main-div">
    <div class="icon">
      <font-awesome-icon :icon="['fas', iconName]" />
    </div>
    <p>{{ text }}</p>
  </div>
</template>

<script>
export default {
  name: 'Icon',
  props: {
    iconName: String,
    text: String,
    value: String,
  },
  methods: {
    onClick() {
      this.$emit('onClick', this.value, this.iconName)
    },
  },
}
</script>

<style scoped>
.main-div {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.main-div:hover {
  background-color: grey;
  cursor: pointer;
}

.icon {
  padding-right: 5px;
}
</style>
