<template>
  <WorldButton></WorldButton>
  <CreateWordModal ref="CWModal"></CreateWordModal>
  <CreateWorldButton></CreateWorldButton>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import CreateWordModal from './components/worlds/CreateWordModal.vue';
import CreateWorldButton from './components/worlds/CreateWorldButton.vue'
import WorldButton from './components/worlds/WorldButton.vue'

export default {
  name: 'App',
  components: {
    WorldButton,
    CreateWordModal,
    CreateWorldButton
  },
  methods: {
    displayCreateWorldModal() {
      this.$refs.CWModal.toggleModal();
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
