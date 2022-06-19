<template>
  <div class="form">
    <div class="form-title">{{ title }}</div>
    <input type="text" class="form-input" v-model="inputValue" />
    <button :disabled="inputValue.length === 0" @click="onSubmit">
      {{ button }}
    </button>
  </div>
</template>

<script>
export default {
  name: "Form",
  props: ["title", "button", "action"],
  data() {
    return {
      inputValue: "",
    };
  },
  methods: {
    onSubmit() {
      this.action(this.inputValue);
      this.inputValue = "";
    },
  },
};
</script>

<style>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  justify-content: center;
  margin-top: 20px;
}
.form-input {
  padding: 10px 5px;
  border: 0;
  border-radius: 5px;
  margin: 10px 0px;
  text-align: center;
  color: var(--color-text-dark);
  font-size: 16px;
}
</style>
