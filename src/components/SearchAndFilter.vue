<template>
  <div class="wrapper">
    <div class="filter">
      Amount Filter
      <input v-model="amountFilter" type="number" />
    </div>
    <loading
      v-model:active="isLoading"
      :can-cancel="false"
      :on-cancel="onCancel"
      :is-full-page="false"
    >
    </loading>
    <div class="transaction_list" v-if="items">
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

<script>
import { transactions } from "@/data/transactions";
import Loading from "vue-loading-overlay";
import "vue-loading-overlay/dist/vue-loading.css";

/*
 * I've installed a npm package (vue-loading-overlay)
 * with a loading spinner and tried to simulate api calls with
 * simply activate and deactivate the loading spinner in setTimeout().
 * */
export default {
  name: "SearchAndFilter",
  props: {
    itemId: String,
    itemBackground: String,
  },
  components: { Loading },
  computed: {
    filteredItems() {
      return this.items[this.itemId]?.filter(
        (x) => x.amount >= this.amountFilter
      );
    },
  },
  watch: {
    itemId() {
      this.amountFilter = "";
      this.isLoading = true;
      setTimeout(() => {
        this.items = transactions;
        this.isLoading = false;
      }, 2500);
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
      amountFilter: "",
      items: [],
      isLoading: false,
    };
  },
  methods: {
    onCancel() {
      console.log("cancelled loader.");
    },
  },
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
