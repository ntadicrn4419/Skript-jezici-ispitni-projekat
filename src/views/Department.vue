<template>
  <div>
    <Header :subtitle="subtitle" />
    <ImageList v-if="imageIDs" :objects="imageIDs"/>
  </div>
</template>

<script>
import Header from '@/components/Header.vue';
import ImageList from '@/components/ImageList.vue';


export default {
  name: 'Departments',

  components:{
    Header,
    ImageList
  },

  data(){
    return {
      subtitle: '',
      depID: null,
      imageIDs: null
    }
  },

  watch:{
    $route(){
      this.subtitle = this.$route.params.name;
      this.depID = this.$route.params.id;

      fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects?departmentIds=${this.depID}`)
      .then(o => o.json())
      .then(res => this.imageIDs = res.objectIDs);
    }
  },

  mounted(){
    this.subtitle = this.$route.params.name;
    this.depID = this.$route.params.id;

    fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects?departmentIds=${this.depID}`)
      .then(o => o.json())
      .then(res => this.imageIDs = res.objectIDs);
  }
}
</script>
