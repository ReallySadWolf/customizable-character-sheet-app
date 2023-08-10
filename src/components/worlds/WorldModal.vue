<template>
  <div class="modal fade" id="CreateWorldModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Create a new world</h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div id="alertContainer">
          </div>
          <div class="input-group mb-3">
            <div class="input-group-text" id="basic-addon1">World name</div>
            <input type="text" class="form-control" id="WorldNameInput" placeholder="World name" aria-label="WorldName"
              aria-describedby="basic-addon1" />
          </div>
          <div class="input-group mb-3">
            <div class="input-group-text" id="basic-addon2">World description</div>
            <input type="text" class="form-control" id="WorldDescriptionInput" placeholder="World description"
              aria-label="WorldDescription" aria-describedby="basic-addon2" />
          </div>
          <div class="input-group mb-3">
            <div class="input-group-text" id="basic-addon3">Thumbnail image link</div>
            <input type="text" class="form-control" id="ImgLinkInput" placeholder="Image link" aria-label="ImgLink"
              aria-describedby="basic-addon3" />
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
  name: "WorldModal",
  methods: {
    toggleModal() {
      var myModal = bootstrap.Modal.getOrCreateInstance(
        document.getElementById("CreateWorldModal")
      );
      myModal.toggle();
    },
    toggleEditModal(worldName) {
      var objectString = localStorage.getItem(worldName);
      var obj = JSON.parse(objectString);

      //variables added for better readability
      var worldDescription = obj.description;
      var imgLink = obj.imgLink;

      //remember original key (world name) in an invisible div
      var keyHolder = document.getElementById("origKeyHolder");
      keyHolder.setAttribute("origKey", worldName);

      //set World name field to the current name
      var worldNameInput = document.getElementById("WorldNameInput");
      worldNameInput.value = worldName;

      //set World description field to the current name
      var worldDescriptionInput = document.getElementById("WorldDescriptionInput");
      worldDescriptionInput.value = worldDescription;

      //set World name field to the current name
      var imgLinkInput = document.getElementById("ImgLinkInput");
      imgLinkInput.value = imgLink;

      var myModal = bootstrap.Modal.getOrCreateInstance(
        document.getElementById("CreateWorldModal")
      );
      myModal.toggle();
    },
    createWorld() {
      var alertContainer = document.getElementById("alertContainer");
      var worldName = document.getElementById("WorldNameInput").value;
      if (worldName == "") {
        var alertNode = document.createElement("div");
        alertNode.setAttribute("class", "alert alert-danger");
        alertNode.setAttribute("role", "alert");
        alertNode.innerHTML = "World name has to have at least one character.";
        alertContainer.appendChild(alertNode);
      } else {
        var jsonObj = { "description": "", "imgLink": "" };
        jsonObj.description = document.getElementById("WorldDescriptionInput").value;
        jsonObj.imgLink = document.getElementById("ImgLinkInput").value;
        localStorage.setItem(worldName, JSON.stringify(jsonObj));
        var myModal = bootstrap.Modal.getOrCreateInstance(
          document.getElementById("CreateWorldModal")
        );
        myModal.toggle();
      }
    },
  },
};
</script>

