<template>
    <WorldsGrid ref="WorldsGrid" :key="componentKey"></WorldsGrid>
    <WorldModal ref="WorldModal"></WorldModal>
    <CreateWorldButton></CreateWorldButton>
</template>
  
<script>
//import HelloWorld from './components/HelloWorld.vue'
import WorldModal from './components/worlds/WorldModal.vue'
import WorldsGrid from './components/worlds/WorldsGrid.vue';
import CreateWorldButton from './components/worlds/CreateWorldButton.vue';

export default {
    name: 'WorldsPage',
    components: {
        WorldsGrid,
        WorldModal,
        CreateWorldButton
    },
    methods: {
        displayCreateWorldModal() {
            this.$refs.WorldModal.toggleModal();
        },
        displayEditWorldModal(worldName) {
            console.log(worldName);
            this.$refs.WorldModal.toggleEditModal(worldName);
        },
        deleteWorld(worldName) {
            var elementToDelete = document.getElementById(worldName);
            elementToDelete.remove();
        },
        reloadGrid() {
            this.componentKey += 1;
        },
        setViewedWorld(worldName) {
            this.$parent.setViewedWorld(worldName);
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
  