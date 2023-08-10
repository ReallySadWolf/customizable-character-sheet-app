<template>
    <div class="d-grid gap-2 col-1 mx-auto">
      <button type="button" name="createNewWorld" id="createNewWorld" class="btn btn-success" @click="displayModal">Create a new world</button>
    </div>
</template>

<script>
export default {
    name: 'CreateWorldButton',
    methods: {
        displayModal() {
            this.$parent.displayCreateWorldModal();
        }
    }
}

</script>