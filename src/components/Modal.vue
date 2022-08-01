<template>
  <div class="backdrop" @click.self="closeModal">
    <div class="modal">
      <h1>{{ header }}</h1>
      <p>{{ content }}</p>
      <slot>Default slot content</slot>
      <slot name="form"></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: ["header", "content"],
  data() {
    return {
	  name: ""
	}
  },
  methods: {
    closeModal() {
      this.$emit("close");
    },
	submitModal() {
	  console.log("Submit name " + name);
	  this.$emit("submittt", name);
	}
  },
};
</script>

<style scoped>
.modal {
  width: 400px;
  padding: 20px;
  margin: 100px auto;
  background: white;
  border-radius: 10px;
}
.backdrop {
  position: fixed;
  top: 0;
  background: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
}
h1 {
  color: blue;
}
</style>
