<template>
<input :min="min"
    :max="max"
    :step="step"
    :value="value"
    @input="onButtonRange">
</template>

<script>


export default {
name: 'CustomRange',
  props: {
    value: Number,
    min: Number,
    max: Number,
    step: Number,
  },
  methods: {
    onButtonRange(event) {
      this.$emit('input', event.target.value);
    }
  }
}

</script>

<style lang="scss" scoped>

</style>