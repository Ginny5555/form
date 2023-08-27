<template>
  <input
    :type="type"
    :placeholder="placeholder"
    :value="modelValue"
    @input="onInputChange"
    :maxlength="maxlength"
    :minlength="minlength"
    :class="{ 'error-border': error && showError }"
    @focus="showError = true"

  />
</template>

<script>
export default {
  name: "CustomInput",
  data(){
    return {
         showError:false,
    }

  },
  emits: ["update:modelValue"],
  props: {
    type: {
      type: [Number, String],
      default: "text"
    },
    placeholder: {
      type: String,
      required: true
    },
    label: {
      type: String,
      required: true
    },
    maxlength: {
      type: [Number, String],
      required: false
    },
    minlength: {
      type: [Number, String],
      required: false
    },
    value: {
      type: [Number, String]
    },
    modelValue: {
      type: [Number, String]
    },
    error: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    onInputChange(event) {
      const value = event.target.value;

      this.$emit("update:modelValue", value);

      // this.$emit("errorChange", this.error);
    }
  }
};
</script>

<style lang="scss" scoped>
input {
  border-radius: 6px;
  padding: 5px;
  border: 1px solid rgba(5, 128, 130, 0.267);
  margin: 10px 0px;
}
.error-border {
  border: 1px solid red;
}
</style>