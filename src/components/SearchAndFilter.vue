<template>
  <div class="wrapper">
    <div class="filter">
      Amount Filter
      <input v-model="state.amountFilter" type="number" />
      {{ state.amountFilter }}
    </div>
    <loading
      v-model:active="isLoading"
      :can-cancel="false"
      :on-cancel="onCancel"
      :is-full-page="false"
    >
    </loading>
    <div class="transaction_list" v-if="state.items">
      <div
        class="item"
        v-for="item in filteredItems"
        :key="item.id"
        :style="{ backgroundColor: itemBackground }"
      >
        <div class="content">
          <span>{{ item.description }}</span>
          <span>{{ item.amount }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, computed, defineProps, watch, ref } from "vue";
import { ITransaction } from "@/interfaces/ITransaction";
import { transactions } from "@/data/transactions";

import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";

const props = defineProps({
  itemId: String,
});

const itemId = ref("");

const state = reactive({
  amountFilter: "",
  items: [] as Array<ITransaction>,
  isLoading: false,
});

const filteredItems = computed(() => {
  console.log(props.itemId);
  return "";
  /*return state.items[props.itemId].filter(
    (x) => x.amount >= state.amountFilter
  );*/
});

watch(itemId, () => {
  state.amountFilter = "";
  state.isLoading = true;
  setTimeout(() => {
    state.items = transactions;
    state.isLoading = false;
  }, 2500);
});
/*
name: "SearchAndFilter",
  props: {
  itemId: String,
    itemBackground: String,
},
components: { Loading },
computed: {
  filteredItems(): any[] {

  },
},
watch: {
  itemId() {

  },
},
created() {
  this.isLoading = true;
  setTimeout(() => {
    this.isLoading = false;
  }, 5000);
},
data() {
  return {
    amountFilter: "" as string,
    items: [] as Array<ITransaction>,
    isLoading: false,
  };
}*/
const onCancel = () => {
  console.log("cancelled loader.");
};
</script>

<style scoped lang="scss">
.wrapper {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;

  .filter {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;

    input {
      height: 20px;
      border-radius: 5px;
      min-width: 200px;
      width: 500px;
      border-color: #148dea;
    }
  }
  .transaction_list {
    margin-top: 1em;
    .item {
      margin: 0.5em;
      width: 500px;
      border: 1px solid #fff;
      height: 50px;
      border-radius: 5px;
      padding: 0 0.5em;
      .content {
        height: 100%;
        display: flex;
        justify-content: space-between;
        justify-items: center;
        align-items: center;

        span {
          &:first-child {
            font-weight: bold;
          }
        }
      }
    }
  }
}
</style>
