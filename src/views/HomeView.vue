<template>
  <div class="home">
    <div class="cards">
      <CardView
        v-for="(card, index) of cardData"
        :key="index"
        :card-id="card.id"
        :card-description="card.description"
        :style="{ backgroundColor: cardColors[index] }"
        @click="getSelectedCard(card.id, cardColors[index])"
      ></CardView>
    </div>
    <hr />
    <SearchAndFilter
      :itemId="selectedCardId"
      :itemBackground="selectedCardColor"
    ></SearchAndFilter>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { cards } from "@/data/cards";
import CardView from "@/components/Card.vue";
import SearchAndFilter from "@/components/SearchAndFilter.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    CardView,
    SearchAndFilter,
  },
  data() {
    return {
      cardData: cards,
      cardColors: ["#f3f4f4", "#148dea"],
      selectedCardId: "",
      selectedCardColor: "",
    };
  },
  methods: {
    getSelectedCard(cardId: string, cardColor: string) {
      this.selectedCardId = cardId;
      this.selectedCardColor = cardColor;
    },
  },
});
</script>
<style lang="scss">
.home {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;

  .cards {
    display: flex;
    align-items: center;
    justify-content: center;
  }
}
</style>
