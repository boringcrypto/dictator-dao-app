<style lang="scss">
@import "src/scss/main.scss";
</style>

<template>
  <div class="text-center">
    <img alt="Dictator DAO Logo" src="./assets/logo.jpeg" height="180" />
    <h1>Dictator DAO</h1>

    <p>
      Dictator DAO is an organization where the token holders democratically
      elect a 'dictator' to operate the protocol. Whenever the DAO isn't happy,
      they can simply elect a new 'dictator'.
    </p>
    <Web3 :info="web3">
      <template v-slot:none>
        No web3 provider was found. Please use MetaMask.
      </template>
      <template v-slot:connect>
        <button @click="web3.connect">Connect Metamask</button>
      </template>
      <table class="table mx-auto text-start" style="width: 600px">
        <tr>
          <td>Name</td>
          <td>{{ web3.name }}</td>
        </tr>
        <tr>
          <td>Connected</td>
          <td>{{ web3.connected }}</td>
        </tr>
        <tr>
          <td>Address</td>
          <td>{{ web3.address }}</td>
        </tr>
        <tr>
          <td>ChainId</td>
          <td>{{ web3.chainId }}</td>
        </tr>
        <tr>
          <td>Block</td>
          <td>{{ web3.block }}</td>
        </tr>
      </table>
    </Web3>
  </div>
</template>

<script lang="ts">
import { defineComponent, Ref, ref } from "vue";
import Web3, { EmptyProviderInfo, ProviderInfo } from "./components/Web3.vue";

export default defineComponent({
  name: "App",
  components: {
    Web3,
  },
  setup: () => {
    const web3: Ref<ProviderInfo> = ref(EmptyProviderInfo);
    return {
      web3,
    };
  },
});
</script>
