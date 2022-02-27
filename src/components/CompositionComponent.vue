<template>
  <q-header bordered class="my-header">
    <MyModal
      v-show="isVisible"
      :selected_prop="selected"
      :close="close"
      :removeSelected="removeSelected"
    />
  </q-header>

  <q-page class="q-pa-md container">
    <q-table
      grid
      card-class="bg-primary "
      :rows="getData"
      row-key="id"
      hide-header
      virtual-scroll
      :rows-per-page-options="[0]"
    >
      <template v-slot:item="props">
        <div class="q-pa-md q-gutter-md justify-content-center">
          <q-card
            class="my-card shadow-15 round-5 q-pa-md row"
            v-bind:border-new="props.row.new === true"
          >
            <q-item class="left-card-con col">
              <q-item-section class="avatar" avatar>
                <!-- <q-avatar color="primary" size="60px" icon="props.row.logo" /> -->
                <q-img :src="props.row.logo" style="width: 70px" />
              </q-item-section>

              <q-item-section>
                <div class="bejo row">
                  <q-item-label
                    class="text-weight-bold bejo-child text-primary text-subtitle-2"
                    >{{ props.row.company }}
                  </q-item-label>

                  <p
                    v-show="props.row.new"
                    class="bg-primary new-btn round"
                    color="accent"
                  >
                    NEW!
                  </p>

                  <p
                    v-show="props.row.featured"
                    class="bg-dark featured-btn"
                    color="accent"
                  >
                    FEATURED
                  </p>
                </div>

                <q-item-label class="text-weight-bold text-black q-mb-sm">
                  {{ props.row.position }}
                </q-item-label>

                <q-item-section>
                  <q-item-label caption class="q-p-l-large">
                    {{ props.row.postedAt }} • {{ props.row.contract }} •

                    {{ props.row.location }}
                  </q-item-label>
                </q-item-section>
              </q-item-section>
            </q-item>

            <q-item class="col tag-container">
              <q-item-section
                v-for="tool in props.row.tools"
                :key="tool"
                horizontal
                class="tools-parent"
              >
                <q-btn
                  flat
                  round-10
                  class="bg-secondary my-btn text-capitalize"
                  color="primary"
                  :value="tool"
                  @click="handleChange(tool)"
                >
                  {{ tool }}
                </q-btn>
              </q-item-section>

              <q-item-section
                v-for="lang in props.row.languages"
                :key="lang"
                horizontal
                class="tools-parent"
              >
                <q-btn
                  flat
                  round-10
                  class="bg-secondary my-btn text-capitalize"
                  color="primary"
                  @click="handleChange(lang)"
                >
                  {{ lang }}
                </q-btn>
              </q-item-section>

              <q-item-section class="tools-parent">
                <q-btn
                  flat
                  round-10
                  class="bg-secondary my-btn text-capitalize"
                  color="primary"
                  @click="handleChange(props.row.level)"
                >
                  {{ props.row.level }}
                </q-btn>
              </q-item-section>

              <q-item-section class="tools-parent">
                <q-btn
                  flat
                  round-10
                  class="bg-secondary my-btn text-capitalize"
                  color="primary"
                  @click="handleChange(props.row.role)"
                >
                  {{ props.row.role }}
                </q-btn>
              </q-item-section>
            </q-item>
          </q-card>
        </div>
      </template>
    </q-table>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, PropType, computed, ref } from 'vue';
import { Listings } from './models';
import MyModal from './MyModal.vue';

export default defineComponent({
  name: 'CompositionComponent',
  components: { MyModal },
  props: {
    rows: {
      type: Array as PropType<Listings[]>,

      required: true,
    },

    active: {
      type: Boolean,
    },
  },
  setup(props) {
    let selected = ref<Array<string>>([]); //array with clicked tags

    const handleChange = (e: string) => {
      //active to true  switches from full list to filtered list
      //tags clicked will the added in array excluding duplicates

      active.value = false;
      if (!selected.value.includes(e)) {
        selected.value.push(e);
        active.value = true;
        open();
        return;
      }
    };

    const active = ref(false);
    const isVisible = ref(false);
    const open = () => (isVisible.value = true);
    const close = () => {
      //closes modal and empties tags list
      isVisible.value = false;
      selected.value = [];
      active.value = false;
    };
    const removeSelected = (e: number) => {
      selected.value.splice(e, 1);
      if (selected.value.length < 1) {
        close();
      }

      return;
    };

    let filteredResult = () => {
      const result3 = props.rows.filter((item) =>
        selected.value.some((val) => item.languages.includes(val))
      );
      const result1 = props.rows.filter((item) =>
        selected.value.some((val) => item.tools.includes(val))
      );
      const result2 = props.rows.filter((item) =>
        selected.value.some((val) => item.level.includes(val))
      );
      const result4 = props.rows.filter((item) =>
        selected.value.some((val) => item.role.includes(val))
      );
      const resultList = [result1, result2, result3, result4];
      //some arrays will be empty so we remove them here.
      let filteredResult = resultList.find((a) => a.length > 1);

      return filteredResult;
    };

    const getData = computed(() => {
      //we can either get the original data props.rows or the filtered
      //if a tag is clicked it triggers the active.value to true so that we can switch
      if (active.value === false) {
        return props.rows;
      } else {
        return filteredResult();
      }
    });
    return {
      handleChange,
      removeSelected,
      getData,
      selected,
      filteredResult,
      isVisible,
      close,
    };
  },
});
</script>

<style lang="scss">
.my-header {
  background: url('../assets/images/bg-header-desktop.svg');
  background-color: $primary;
  height: 9em;
}
.container {
  margin-inline: auto;
  width: 800px;
  [border-new='true'] {
    border-left: solid 3px $primary;
  }

  .my-card {
    margin-inline: auto;
    width: 750px;

    .left-card-con {
      .bejo {
        gap: 1em;
        .new-btn,
        .featured-btn {
          border-radius: 10px;
          padding-inline: 0.5em;
          line-height: 1.5;
          padding-block: 0.1em;
          margin-block: 0.5em;
          color: white;
          font-size: smaller;
          font-weight: bold;
        }
        .bejo-child {
          margin-block: 0.25em;
          padding-block: 0.25em;
        }
        padding: 0;
        margin: 0;
      }
    }

    .tag-container {
      flex-wrap: wrap;
    }

    .active {
      color: $accent;
      background-color: $primary;
    }
  }
  .tools-parent {
    flex: none;
  }
}
@media (max-width: 750px) {
  .my-header {
    background: url('../assets/images/bg-header-mobile.svg');
    background-color: $primary;
    height: 9em;
  }
  .container {
    outline: solid salmon;
    .q-table--grid .q-table__grid-content {
      justify-content: center;

      .my-card {
        max-width: 400px;
        margin-right: auto;
        flex-direction: column;
        .left-card-con {
          .avatar {
            position: absolute;
            top: -40px;
          }
          border-bottom: solid 1px $accent;
          min-height: 120px;
          padding-top: 1.5em;
        }
        .tag-container {
          min-height: 120px;
        }
      }
    }
  }
}
</style>
