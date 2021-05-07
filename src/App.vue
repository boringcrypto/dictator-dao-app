<style lang="scss">
@import "src/scss/main.scss";
</style>

<template>
  <div class="text-center">
    <img alt="Dictator DAO Logo" src="./assets/logo.jpeg" height="180" />

    <Web3 :info="web3">
      <template v-slot:none>No web3 provider was found. Please use MetaMask.</template>
      <template v-slot:connect>
        <button class="btn btn-primary" @click="web3.connect">Connect Metamask</button>
      </template>
      <router-view :info="web3"></router-view>
    </Web3>
  </div>
</template>

<script lang="ts">
import { BigNumber } from "@ethersproject/bignumber";
import { defineComponent, Ref, ref } from "vue";
import { DictatorToken__factory } from "./assets/ethers-contracts";
import CreateDao from "./components/CreateDao.vue";
import Home from "./pages/Home.vue";
import Web3, { EmptyProviderInfo, ProviderInfo } from "./components/Web3.vue";

export default defineComponent({
  name: "App",
  components: {
    Web3,
    Home,
    CreateDao
  },
  methods: {
    test: async function() {
      if (!window.provider) { return }
      const dao = DictatorToken__factory.connect("0x0a1dda7149fee6c47770609ccd205ff0efe7f761", window.provider)
      this.totalSupply = await dao.totalSupply()
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
