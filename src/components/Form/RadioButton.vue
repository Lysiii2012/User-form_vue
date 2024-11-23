<template>
  <div class="radio-container">
    <h4>Show your profile in Launchpad?</h4>
    <label>
      <input
        type="radio"
        name="profile"
        value="private"
        v-model="radioBtn"
        :disabled="disabled"
      />
      Private
    </label>
    <label>
      <input
        type="radio"
        name="profile"
        value="public"
        v-model="radioBtn"
        :disabled="disabled"
      />
      Public
    </label>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      default: "private",
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  computed: {
    radioBtn: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("update:value", value);
      },
    },
  },
};
</script>

<style scoped>
input {
  appearance: none;
  border: 2px solid #49535c;
  border-radius: 50%;
  width: 20px;
  height: 20px;
  background-color: #ffffff00;
  transition: background-color 0.3s, border-color 0.3s;
}
input:disabled {
  cursor: not-allowed;
}
.radio-container {
  margin-bottom: 32px;
}
input[type="radio"]:checked {
  background: radial-gradient(
    circle,
    rgba(73, 83, 92, 1) 40%,
    rgba(2, 0, 36, 0) 51%
  );
  border-color: #49535c;
}
.radio-container input[type="radio"]:focus {
  outline: none;
  border-color: #49535c;
}

.radio-container input[type="radio"]:hover {
  border-color: #49535c;
}
h4 {
  margin-bottom: 16px;
}
.radio-container label {
  font-family: "Roboto";
  font-size: 20px;
  font-weight: 400;
  line-height: 32px;
  color: #49535c;
}
</style>
