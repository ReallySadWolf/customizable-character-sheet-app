<template>
    <div class="col" v-bind:id="characterName">
        <div class="card shadow-sm text-center" style="width: 20rem;">
            <div class="card-body" :style="{backgroundImage: image}">
                <h5 class="card-title"> {{ characterName }}</h5>
                <div class="d-flex justify-content-between align-items-center">
                    <div class="btn-group">
                        <a :href="window.location.pathname + '/' + characterName">
                            <button type="button" class="btn btn-primary" v-bind:value="characterName">
                                <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                    class="bi bi-arrow-right-square" viewBox="0 0 16 16">
                                    <path fill-rule="evenodd"
                                        d="M15 2a1 1 0 0 0-1-1H2a1 1 0 0 0-1 1v12a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1V2zM0 2a2 2 0 0 1 2-2h12a2 2 0 0 1 2 2v12a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2V2zm4.5 5.5a.5.5 0 0 0 0 1h5.793l-2.147 2.146a.5.5 0 0 0 .708.708l3-3a.5.5 0 0 0 0-.708l-3-3a.5.5 0 1 0-.708.708L10.293 7.5H4.5z" />
                                </svg>
                            </button>
                        </a>
                        <button type="button" class="btn btn-danger" v-bind:value="title" @click="deleteCharacter(characterName)">
                            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
                                class="bi bi-trash-fill" viewBox="0 0 16 16">
                                <path
                                    d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1H2.5zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5zM8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5zm3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0z" />
                            </svg>
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default{
    name: "CharacterButton",
    props: {
        worldName: String,
        characterName: String,
        imgLink: String
    },
    methods:{
        deleteCharacter(characterName){
            var jsonString = localStorage.getItem(this.worldName);
            var jsonObj = JSON.parse(jsonString);
            delete jsonObj.characters[characterName];
            localStorage.setItem(this.worldName, JSON.stringify(jsonObj));
        }
    },
    computed: {
        image: function() {
            if (this.imgLink != ""){
                return this.imgLink;
            }
            else {
                return "@/assets/svg.svg"
            }
        }
    }
}
</script>