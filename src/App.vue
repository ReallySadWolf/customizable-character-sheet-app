<template>
  <WorldsPage></WorldsPage>
</template>

<script>


export default {
  name: 'App',
  components: {
    
  },
  methods: {
    displayCreateWorldModal() {
      this.$refs.WorldModal.toggleModal();
    },
    displayEditWorldModal(worldName){
      console.log(worldName);
      this.$refs.WorldModal.toggleEditModal(worldName);
    },
    deleteWorld(worldName){
      var elementToDelete = document.getElementById(worldName);
      elementToDelete.remove();
    },
    reloadGrid(){
      this.componentKey += 1;
    }
  },
  data() {
    return {
      componentKey: 0
    }
  }
};
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
