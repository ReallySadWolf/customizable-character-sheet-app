<template>
    <div class="album py-5 bg-light">
        <div class="container">
            <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3" id="rows">
                <WorldButton v-for="({ title, description, imgLink }, i) in worlds" :key="i" v-bind:title="title"
                    v-bind:description="description" v-bind:imgLink="imgLink"></WorldButton>
            </div>
        </div>
    </div>
</template>

<script>

import WorldButton from './WorldButton.vue';

export default {
    name: "WorldsGrid",
    components: {
        WorldButton
    },
    methods: {
        deleteWorld() {
            this.$parent.reloadGrid();
        },
        displayEditWorldModal(worldName) {
            this.$parent.displayEditWorldModal(worldName);
        }
    },
    computed: {
        rowElement: function () {
            return document.getElementById("rows");
        },
        worlds: function () {
            var worlds = []

            for (var i = 0; i < localStorage.length; i++) {
                var jsonObj = JSON.parse(localStorage.getItem(localStorage.key(i)));
                jsonObj.title = localStorage.key(i);
                worlds.push(jsonObj);
            }

            return worlds;
        }
    },
    data() {
        return {
            componentKey: 0
        };
    }
}
</script>