<template>
  <div class="input-wrapper">
    <input
      :type="type"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
      :placeholder="placeholder"
      :required="required"
      :disabled="disabled"
      class="input-field"
    />
    <p v-if="error" class="input-error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  props: {
    modelValue: {
      type: String,
      required: false,
      default: "",
    },
    type: {
      type: String,
      required: false,
      default: "",
    },
    placeholder: {
      type: String,
      required: false,
      default: "",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
    required: {
      type: Boolean,
      required: false,
      default: false,
    },
    error: {
      type: String,
      required: false,
      default: "",
    },
  },
};
</script>

<style scoped>
.input-field {
  margin-bottom: 28px;
  border: 1.41px solid #00000061;
  border-radius: 11.3px;
  background: transparent;
  font-family: "Roboto";
  font-size: 22.6px;
  font-weight: 400;
  line-height: 32.49px;
  height: 80px;
  box-sizing: border-box;
  width: 100%;
  padding: 0 19px;
  display: flex;
  align-items: center;
}
.input-error {
  color: red;
  font-size: 12px;
}
</style>
