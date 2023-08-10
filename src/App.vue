<template>
  <WorldButton title="Working title" description='working description of the Mini. World asdf' imgLink="https://cdnb.artstation.com/p/assets/images/images/056/614/903/large/deep-voyage-stunning-anime-landscape.jpg?1669693899"></WorldButton>
  <WorldModal ref="CWModal"></WorldModal>
  <CreateWorldButton></CreateWorldButton>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import WorldModal from './components/worlds/WorldModal.vue';
import CreateWorldButton from './components/worlds/CreateWorldButton.vue'
import WorldButton from './components/worlds/WorldButton.vue'

export default {
  name: 'App',
  components: {
    WorldButton,
    WorldModal,
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
