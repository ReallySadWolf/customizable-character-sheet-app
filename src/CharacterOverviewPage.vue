<template>
 <div></div>
</template>

<script>

export default{
    name: 'CharacterOverviewPage',
    components:{

    },
    methods:{

    },
    computed:{
        worldName: function() {
            return window.location.pathname.split('/')[1];
        },
        characterList: function() {
            var jsonString = localStorage.getItem(this.worldName);
            var jsonObj = JSON.parse(jsonString);
            return jsonObj.characters;
        }
    }
}
</script>