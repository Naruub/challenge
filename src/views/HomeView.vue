<template>
  <div class="home">
    <CardView
      v-for="(card, index) of cardData"
      :key="index"
      :card-id="card.id"
      :card-description="card.description"
    ></CardView>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { cards } from "@/data/cards";
import CardView from "@/components/Card.vue";

export default defineComponent({
  name: "HomeView",
  components: {
    CardView,
  },
  data() {
    return {
      helloDkb: "hello dkb",
      cardData: cards,
    };
  },
  methods: {},
});
</script>
<style lang="scss">
.home {
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
