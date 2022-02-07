<template>
  <div>
    <Header :subtitle="subtitle"/>
    <div v-if="image">
      <img v-if="image.primaryImageSmall" :src="image.primaryImageSmall" />
      <p v-else>Image not available</p>
      
      <ul>
        <li>Author: {{ image.artistDisplayName }}</li>
        <li>Highlight: {{ image.isHighlight }}</li>
        <li>Year acquired: {{ image.accessionYear }}</li>
      </ul>
    </div>
  </div>
</template>

<script>

  import Header from '@/components/Header.vue';

  export default {
    name: 'Single',

    components: {
      Header
    },

    data() {
      return {
        image: null,
        subtitle: ''
      }
    },
    
    mounted() {
      fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects/${this.$route.params.id}`)
        .then( obj => obj.json() )
        .then( res => {
          this.image = res;
          this.subtitle = this.image.title;
        });
    }
  }

</script>