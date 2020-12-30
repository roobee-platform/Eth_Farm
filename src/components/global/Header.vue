<template>
  <header class="header">
    <div class="container">
      <div class="header__inner">
        <router-link :to="{name: 'index'}" class="header__logo">
          <img src="../../assets/images/logo.svg" alt="roobee">
        </router-link>
        <nav class="header__nav">
          <router-link :to="{name: 'index'}" class="header__link header__link--active">Home</router-link>
          <router-link :to="{name: 'farming'}" class="header__link">Farming</router-link>
          <router-link :to="{name: 'about'}" class="header__link">About</router-link>
          <a href="https://bsc.roobee.finance/" class="header__link">BSC Network</a>
        </nav>
        <div class="header__box">
          <a href="#" class="button header__button" @click.prevent="showModal" :class="{'button--green': metamaskAccount}">{{ metamaskAccount ? `${metamaskAccount.substring(0, 6 + 2)}...${metamaskAccount.substring(42 - 6)}` : 'Unlock wallet' }}</a>
          <div class="header__menu">
            <div class="header__menu-icon" @click="menuStatus =! menuStatus"></div>
            <transition name="fade">
              <div class="header__list" v-if="menuStatus">
                <router-link :to="{name: 'index'}" class="header__link header__link--active">Home</router-link>
                <router-link :to="{name: 'farming'}" class="header__link">Farming</router-link>
                <router-link :to="{name: 'about'}" class="header__link">About</router-link>
                <a href="https://bsc.roobee.finance/" class="header__link">BSC Network</a>
              </div>
            </transition>
          </div>
        </div>
      </div>
    </div>
    <WalletModal ref="modal"/>
  </header>
</template>

<script>
import WalletModal from "@/components/WalletModal";
import {mapState} from 'vuex'

export default {
  name: "Header",
  components: {
    WalletModal,
  },

  data: function () {
    return {
      menuStatus: false
    }
  },

  computed: {
    ...mapState(['metamaskAccount'])
  },

  methods: {
    showModal: function () {
      this.$refs.modal.show = true
    },
  }
}
</script>

<style>

</style>