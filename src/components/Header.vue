<template>
    <div class="title">
        <h1>The tennis coaches association</h1>
        <h3 v-if="subtitle">{{ subtitle }}</h3>   
    </div>
</template>

<script>

export default {
   name: 'Header',
   props: {
       subtitle: String
   }
}
</script>

<style scoped>
    .title{
        padding-top: 15px;
        margin-bottom: 25px;
    }
</style>
