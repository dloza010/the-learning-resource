<template>
    <ul>
        <learning-resource 
        v-for="resource in resources" 
        :id="resource.id"
        :key="resource.id"
        :title="resource.title"
        :description="resource.description"
        :link="resource.link"
        ></learning-resource>
    </ul>
</template>

<script>
import LearningResource from './learning-resources/LearningResource.vue';
export default{
    components:{
        LearningResource
    },
    inject: ['resources']
}
</script>

<style scoped>
ul {
    list-style: none;
    margin: 0;
    padding: 0;
    margin: auto;
    max-width: 40rem;
}
</style>