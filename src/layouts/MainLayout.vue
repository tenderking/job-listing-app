<template>
  <q-layout view="hHh rPr fFf">
   


    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script lang="ts">


import { defineComponent } from 'vue'

export default defineComponent({
  name: 'MainLayout',
})
</script>

<style lang="scss">

</style>