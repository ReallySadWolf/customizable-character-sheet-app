<template>
  <div class="modal fade" id="CreateWorldModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Create a new world</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div class="alert alert-danger fade" tabindex="-1" role="alert">
            A simple danger alert with. Give it a click if you like.
          </div>
          <div class="input-group mb-3">
            <span class="input-group-text" id="basic-addon1">World name</span>
            <input type="text" class="form-control" id="WorldNameInput" placeholder="World name" aria-label="WorldName"
              aria-describedby="basic-addon1" />
          </div>
        </div>
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">
            Close
          </button>
          <button type="button" class="btn btn-primary" @click="createWorld">
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const bootstrap = require("bootstrap");

export default {
  name: "CreateWorldModal",
  methods: {
    toggleModal() {
      var myModal = bootstrap.Modal.getOrCreateInstance(
        document.getElementById("CreateWorldModal")
      );
      myModal.toggle();
    },
    createWorld() {
      var errorText = document.getElementById("ErrorText");
      var worldName = document.getElementById("WorldNameInput").value;
      if (worldName == "") {
        errorText.value = "Invalid name";
      } else {
        localStorage.setItem(worldName, "");
        var myModal = bootstrap.Modal.getOrCreateInstance(
          document.getElementById("CreateWorldModal")
        );
        myModal.toggle();
      }
    },
  },
};
</script>
