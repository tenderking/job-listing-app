<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'MyModal',
  props: {
    title: {
      type: String,
      required: true,
    },
    selected_prop: {
      type: Array,
    },
    close: {
      type: Function,
      required: true,
    },
    removeSelected: {
      type: Function,
      required: true,
    },
  },
});
</script>
<template>
  <q-card class="modal bg-white">
    <q-item class="filter-container">
      <q-btn-group
        flat
        round
        padding="none"
        class="btn__group"
        v-for="(item, index) in selected_prop"
        :key="item"
      >
        <q-btn
          flat
          color="primary"
          class="bg-secondary text-capitalize btn__close--text"
        >
          {{ item }}
        </q-btn>
        <q-btn
          flat
          color="secondary"
          icon-right="close"
          size="sm"
          class="bg-primary btn__close--icon"
          @click="removeSelected(index)"
        />
      </q-btn-group>
    </q-item>
    <q-item>
      <q-btn
        @click="close"
        flat
        color="primary"
        label="clear"
        class="text-capitalize btn__clear"
      />
    </q-item>
  </q-card>
</template>

<style lang="scss">
.modal {
  position: absolute;
  width: 750px;
  height: 75px;
  left: 0;
  right: 0;
  margin-left: auto;
  margin-right: auto;
  top: 50px;
  z-index: 99;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .btn__close--icon:hover {
    color: $primary;
    background: $dark;
  }
}
@media (max-width: 750px) {
  .my-modal {
    width: 100vw;
    height: 100px;
    .filter-container {
      flex-wrap: wrap;
      gap: 0.25em;
    }
  }
}
</style>
