<template>
  <div class="modal fade" id="CreateWorldModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="modalTitle"></h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
        </div>
        <div class="modal-body">
          <div id="alertContainer">
          </div>
          <div id="origKeyHolder" origKey=""></div>
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
          <button type="button" class="btn btn-primary" @click="setWorld">
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
      this.setModalTitle("Create a new world")
      this.clearAlerts();

      //remember original key (world name) in an invisible div
      var keyHolder = document.getElementById("origKeyHolder");
      keyHolder.setAttribute("origKey", "");

      //clear World name field
      var worldNameInput = document.getElementById("WorldNameInput");
      worldNameInput.value = "";

      //clear World description
      var worldDescriptionInput = document.getElementById("WorldDescriptionInput");
      worldDescriptionInput.value = "";

      //clear Img link
      var imgLinkInput = document.getElementById("ImgLinkInput");
      imgLinkInput.value = "";

      //clear 

      var myModal = bootstrap.Modal.getOrCreateInstance(
        document.getElementById("CreateWorldModal")
      );
      myModal.toggle();
    },
    toggleEditModal(worldName) {
      this.setModalTitle("Editng '" + worldName + "'");
      this.clearAlerts();

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
    setWorld() {
      var keyHolder = document.getElementById("origKeyHolder");
      var origKey = keyHolder.getAttribute("origKey");
      var alertContainer = document.getElementById("alertContainer");
      var worldName = this.worldNameInput.value;
      var worldDescription = this.worldDescriptionInput.value;
      var imgLink = this.imgLinkInput.value;
      var alertNode = document.createElement("div");

      //throw an alret if the name is empty
      if (worldName == "") {
        alertNode.setAttribute("class", "alert alert-danger");
        alertNode.setAttribute("role", "alert");
        alertNode.innerHTML = "World name has to have at least one character.";
        alertContainer.appendChild(alertNode);
      } else {
        //creating object
        var jsonObj = { "description": "", "imgLink": "" };
        jsonObj.description = worldDescription;
        jsonObj.imgLink = imgLink;

        if (origKey != "") { //editing an existing world
          var localStorageJsonObj = JSON.parse(localStorage.getItem(origKey));
          localStorageJsonObj.description = jsonObj.description;
          localStorageJsonObj.imgLink = jsonObj.imgLink;
          if (origKey != worldName) {
            localStorage.removeItem(origKey);
          }
          localStorage.setItem(worldName, JSON.stringify(localStorageJsonObj));
        }
        else { //creating a new world
          //check if a world with that name already exists, if it does, throw out an alert
          if (localStorage.getItem(worldName) != null) {
            alertNode.setAttribute("class", "alert alert-danger");
            alertNode.setAttribute("role", "alert");
            alertNode.innerHTML = "A world with this name already exists.";
            alertContainer.appendChild(alertNode);
            return;
          }
          //otherwise create the world
          localStorage.setItem(worldName, JSON.stringify(jsonObj));
        }

        //close the modal
        var myModal = bootstrap.Modal.getOrCreateInstance(
          document.getElementById("CreateWorldModal")
        );
        this.$parent.reloadGrid();
        myModal.toggle();
      }
    },
    clearAlerts() {
      //clear the alertNode
      var alertContainer = document.getElementById("alertContainer");
      if (alertContainer.hasChildNodes()) {
        alertContainer.childNodes.forEach(function (child) {
          child.remove();
        })
      }
    },
    setModalTitle(modalTitle) {
      document.getElementById("modalTitle").innerHTML = modalTitle;
    }
  },
  computed: {
    worldNameInput: function () {
      return document.getElementById("WorldNameInput");
    },
    worldDescriptionInput: function () {
      return document.getElementById("WorldDescriptionInput");
    },
    imgLinkInput: function () {
      return document.getElementById("ImgLinkInput");
    }
  }
};
</script>

