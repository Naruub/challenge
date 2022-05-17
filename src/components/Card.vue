<template>
  <div class="card">
    <p>{{ cardId }}</p>
    <p>{{ cardDescription }}</p>
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
  border: 2px solid #2c3e50;
  border-radius: 5px;
  margin: 1em;
  width: 20em;
  height: 10em;
}
</style>
