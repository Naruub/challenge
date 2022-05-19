<template>
  <div class="card">
    <p>{{ cardDescription }}</p>
    <p>{{ cardId }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CardView",
  props: {
    cardId: {
      type: String,
      required: true,
    },
    cardDescription: {
      type: String,
      required: true,
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.card {
  display: flex;
  flex-direction: column;
  align-items: baseline;
  font-weight: 600;
  border: 2px solid #fff;
  border-radius: 15px;
  margin: 1em;
  width: 20em;
  height: 10em;
  padding: 1em;
}
</style>
