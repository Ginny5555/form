<template>
  <div class="form">
    <CustomInput
      label="Firstname"
      @input="handleInput"
      placeholder="firstname"
      v-model="form.firstname"
      type="text"
      :error="isFirstNameInvalid()"
    />
    <CustomInput
      label="Lastname"
      placeholder="lastname"
      @input="handleInput"
      v-model="form.lastname"
      type="text"
      :error="isLastNameInvalid()"
    />

    <CustomRange
      type="range"
      :min="20"
      :max="100"
      :step="5"
      @input="logCoverageValue"
      v-model="form.coverage"
    />
    <p>{{form.coverage}}</p>
    <p
      v-show="isFormInvalid()"
      :class="{warning:isFormInvalid(), hidden:!isFormInvalid()}"
    >must be less 5 characters and longer than 2</p>
    <CustomButton @click="submitForm" :disabled="isFormInvalid()" />
  </div>
</template>

<script>
// validation rules: firstname - max (5 symbols), min (2), lastname - max (5), min (2)
/*
 * vue-3 emits modelValue
 * custom components (Range, Button, Input)
 * console.log form data after validation and submit
 *
 * */
import CustomButton from "@/components/ui/CustomButton.vue";
import CustomInput from "@/components/ui/CustomInput.vue";
import CustomRange from "@/components/ui/CustomRange.vue";
export default {
  components: {
    CustomButton,
    CustomInput,
    CustomRange
  },
  data() {
    return {
      form: {
        firstname: "",
        lastname: "",
        coverage: 20 //Range [from 0 to 20]
      },

    };
  },

  methods: {
    isFirstNameInvalid() {
      return this.form.firstname.length < 2 || this.form.firstname.length > 5;
    },

    isLastNameInvalid() {
      return this.form.lastname.length < 2 || this.form.lastname.length > 5;
    },

    isFormInvalid() {
      return this.isFirstNameInvalid() || this.isLastNameInvalid();
    },
    logCoverageValue() {
      this.form.coverage = parseInt(event.target.value);
    },
    handleInput(event) {
      const inputField = event.target;
      const maxLength = parseInt(inputField.getAttribute("maxlength"));

      if (maxLength && inputField.value.length > maxLength) {
        inputField.value = inputField.value.slice(0, maxLength);
      }

      // Remove non-letter characters from the input value
      inputField.value = inputField.value.replace(/[^a-zA-Z]/g, "");

      // Update the form data
    },
    submitForm() {
      if (this.isFormInvalid()) {
        console.log("Form data is invalid.");
        return;
      }

      console.log("Form data submitted:", this.form);

      this.form = {
        firstname: "",
        lastname: "",
        coverage: ""
      };
    }
  },

};
</script>

<style lang="scss" scoped>
.form {
  display: flex;
  width: 200px;
  flex-direction: column;
  margin: 0 auto;
  height: 150px;
  justify-content: space-between;
}
.warning {
  font-size: 10px;
  color: red;
  display: block;
}
.hidden {
  display: none;
}
</style>