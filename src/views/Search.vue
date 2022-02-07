<template>
  <div>
    <Header :subtitle="subtitle" />
    <ImageList v-if="imageIDs"  :objects="imageIDs" />
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import ImageList from '@/components/ImageList.vue';

export default {
  name: 'Search',

  components:{
    Header,
    ImageList
  },

  data(){
    return {
      subtitle: 'Search results: ',
      imageIDs: null
    }
  },

  mounted(){
    fetch(`http://colectionapi.metmuseum.org/public/collection/search?q=${this.$route.query.q}`)
    .then(obj => obj.json())
    .then(res => {
      this.subtitle += res.total;
      this.imageIDs = res.objectIDs;
    })
  }
}
</script>
