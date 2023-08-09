<template>
    <div class="container row border align-items-center col-md-5">
        <div class="col-5">
            Name of the World
        </div>
        <div class="col-auto me-auto">
            <button type="button" name="edit" class="btn btn-primary">Edit</button>
        </div>
        <div class="col-auto me-auto">
            <button type="button" name="delete" class="btn btn-danger">Delete</button>
        </div>
    </div>
</template>

<script>

export default{
    name: "WorldButton"
}
</script>