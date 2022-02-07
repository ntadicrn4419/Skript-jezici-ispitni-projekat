<template>
  <div>
    <b-pagination
      v-model="currentPage"
      :total-rows="objects.length"
      :per-page="perPage"
      aria-controls="image-table"
    ></b-pagination>
    <b-table
      id="image-table"
      hover
      fixed
      :items="items"
      :fields="fields"
      small
      :per-page="perPage"
      :current-page="currentPage"
      @row-clicked="rowClicked"
    >
      <template #cell(isHighlight)="data">
        <b-icon v-if="data.value" icon="check-square" variant="success" scale="2"></b-icon>
        <b-icon v-else icon="x-circle" variant="danger" scale="2"></b-icon>
      </template>
    </b-table>
    <b-pagination
      v-model="currentPage"
      :total-rows="objects.length"
      :per-page="perPage"
      aria-controls="image-table"
    ></b-pagination>
  </div>
</template>

<script>

  export default {
    name: 'ImageList',

    data() {
      return {
        fields: ['title', 'artistDisplayName', 'objectDate', 'isHighlight'],
        items: [],
        currentPage: 1,
        perPage: 10
      }
    },
    
    props: {
      objects: Array
    },

    watch: {
      currentPage(nVal, oVal) {
        this.objects.slice(nVal * 10, (nVal + 1) * 10).map( obj => {
          fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects/${obj}`)
            .then( obj => obj.json())
              .then( res => this.items.push(res));
        });
      }
    },

    mounted() {
      this.objects.slice(this.currentPage * 10, (this.currentPage + 1) * 10).map( obj => {
        fetch(`https://collectionapi.metmuseum.org/public/collection/v1/objects/${obj}`)
          .then( obj => obj.json())
            .then( res => this.items.push(res));
      });
    },

    methods: {
      rowClicked(record, index) {
        this.$router.push({ name: 'Single', params: { id: record.objectID } });
      }
    }
  }

</script>

<style scoped>
  .pagination {
    justify-content: center;
  }
</style>