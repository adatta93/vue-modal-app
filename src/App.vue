<template>
  <h1>{{ title }}</h1>
  <teleport to=".modals" v-if="showModal">
    <Modal header="Login to Continue" :content="content" @close="toggleModal">
      <h3>Slot component</h3>
      <template v-slot:form>
        <form @submit.prevent="showContent">
          <input placeholder="Enter Your Name" v-model="name" />
		  <button>Submit</button>
        </form>
      </template>
    </Modal>
  </teleport>
  <button @click.alt="toggleModal">Toggle Modal (alt+click)</button>
  <HelloWorld v-if="showHelloWorld" :msg="helloWorldMsg"></HelloWorld>
</template>

<script>
import Modal from "./components/Modal.vue";
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    Modal,
	HelloWorld
  },
  data() {
    return {
      title: "First Vue Single Page App",
      content: "If you are registered",
      showModal: false,
	  showHelloWorld: false,
	  helloWorldMsg: "Hello World"
    };
  },
  methods: {
    toggleModal() {
      this.showModal = !this.showModal;
    },
	showContent(data) {
	  this.showModal = !this.showModal;
	  this.showHelloWorld = !this.showHelloWorld;
	  console.log(data.target.elements[0].value);
	  let username = data.target.elements[0].value
	  this.helloWorldMsg = "Welcome to Vue, " + username;
	}
  },
};
</script>

<style>
#app,
.modals {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h1 {
  color: red;
}
</style>
