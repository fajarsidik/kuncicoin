<template>
    <div>
        <List :data="list" />
    </div>
</template>
<script>
import List from '../components/List.vue'
import json from '../assets/json/data.json'
export default {
    name: 'Home',
    data(){
        return{
            list : json
        }
    },
    components: {
        List,        
    },
}
</script>
