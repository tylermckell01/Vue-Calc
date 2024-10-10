<template>
  <div class="title">{{ title }}</div>
</template>

<script>
export default {
  name: "CalculatorTitle",
  props: {
    title: {
      type: String,
    },
  },
};
</script>

<style scoped lang="scss">
.title {
}
</style>
