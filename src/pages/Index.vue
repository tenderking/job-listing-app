<template>
  <q-page class="row items-center justify-evenly">
    <example-component
      title="Example component"
      active
     
      :rows="rows"
    ></example-component>
  </q-page>
</template>

<script lang="ts">
import {  Listings } from 'components/models';
import ExampleComponent from 'components/CompositionComponent.vue';
import { defineComponent, ref } from 'vue';
import MyListings from '../data/data.json'



export default defineComponent({
  name: 'PageIndex',
  components: { ExampleComponent },
  setup() {
    const rows= ref<Listings[]>(MyListings)
    
    return {  rows};
  }
});
</script>
