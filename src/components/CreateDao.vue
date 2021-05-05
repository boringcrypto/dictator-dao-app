<template>
  <form class="mx-auto text-start" style="max-width: 400px;">
    <div class="mb-3">
      <label for="inputSymbol" class="form-label">Token Symbol</label>
      <input type="text" v-model="tokenSymbol" class="form-control" id="inputSymbol" />
    </div>

    <div class="mb-3">
      <label for="inputName" class="form-label">Token Name</label>
      <input type="text" v-model="tokenName" class="form-control" id="inputName" />
    </div>

    <div class="mb-3">
      <label for="inputShareSymbol" class="form-label">Staked Token Symbol</label>
      <input type="text" v-model="shareSymbol" class="form-control" id="inputShareSymbol" />
    </div>

    <div class="mb-3">
      <label for="inputShareName" class="form-label">Staked Token Name</label>
      <input type="text" v-model="shareName" class="form-control" id="inputShareName" />
    </div>
  </form>
  <button class="btn btn-primary">Create DAO!</button>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "CreateDao",
  props: {},
  setup: () => {
    const tokenSymbol = "UCT"
    const tokenName = "Umbrella Corporation Token"
    const shareSymbol = "UCS"
    const shareName = "Umbrella Corporation Share"
    return {
      tokenSymbol,
      tokenName,
      shareSymbol,
      shareName
    };
  },
});
</script>