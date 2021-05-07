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
    <create-dao :info="web3"></create-dao>

    <Web3 :info="web3">
      <template v-slot:none>No web3 provider was found. Please use MetaMask.</template>
      <template v-slot:connect>
        <button class="btn btn-primary" @click="web3.connect">Connect Metamask</button>
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
    {{ totalSupply.toString() }}
    <button @click="test">Test</button>
  </div>
</template>

<script lang="ts">
import { BigNumber } from "@ethersproject/bignumber";
import { defineComponent, Ref, ref } from "vue";
import { DictatorDAO, DictatorDAO__factory, DictatorToken__factory } from "./assets/ethers-contracts";
import CreateDao from "./components/CreateDao.vue";
import Web3, { EmptyProviderInfo, ProviderInfo } from "./components/Web3.vue";

export default defineComponent({
  name: "App",
  components: {
    Web3,
    CreateDao,
  },
  methods: {
    test: async function() {
      console.log(window.provider)
      if (!window.provider) { return }
      const dao = DictatorToken__factory.connect("0x0a1dda7149fee6c47770609ccd205ff0efe7f761", window.provider)
      console.log(dao)
      this.totalSupply = await dao.totalSupply()
      console.log(this.totalSupply)
    }
  },
  setup: () => {
    const web3: Ref<ProviderInfo> = ref(EmptyProviderInfo);
    return {
      web3,
      totalSupply: ref(BigNumber.from(0))
    };
  },
});
</script>
