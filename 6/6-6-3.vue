<template>
  <form novalidate>
    <p :class="alertValidation">{{ validMessage }}</p>
    <textarea @input="onInput" :class="textboxValidation"></textarea>
  </form>
</template>

<script>
export default {
  data () {
    return { valid: false }
  },
  computed: {
    validMessage () {
      return this.valid ? '入力されています' : '入力されていません'
    },
    alertValidation () {
      return this.valid ? this.alert.success : this.alert.error
    },
    textboxValidation () {
      return this.valid ? this.textbox.success : this.textbox.error
    }
  },
  methods: {
    isRequired (value) {
      return value.length > 0
    },
    onInput (e) {
      this.valid = this.isRequired(e.target.value)
    }
  }
}
</script>

<style module="alert">
.success {
  color: green;
  font-size: 1.2em;
}
.error {
  font-weight: bold;
  color: red;
  font-size: 2.4em;
}
</style>

<style module="textbox">
.success {
  border: solid 2px navy;
}
.error {
  border: solid 2px orange;
}
</style>

