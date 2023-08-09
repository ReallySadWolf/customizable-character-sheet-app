<template>
    <div class="d-grid gap-2 col-6 mx-auto">
      <button type="button" name="createNewWorld" id="createNewWorld" class="btn btn-primary" @click="displayModal">Create a new world</button>
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