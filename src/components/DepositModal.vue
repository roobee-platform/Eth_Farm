<template>
  <transition name="modal-fade">
    <div class="modal-box " v-if="show" @click.self="closeModal">
      <div class="overlay" @click="show = false"></div>
      <div class="modal">
        <button class="modal__close" @click="show = false">
          <img src="../assets/images/close.svg" alt="">
        </button>
        <div class="modal__container">
          <div class="modal__title">Deposit ROOBEE-ETH LPs Tokens</div>
          <div class="modal__inner">
            <div class="deposit">
              <div class="deposit__range">
                <div class="deposit__text">Available ROOBEE-ETH LPs</div>
                <div class="deposit__text deposit__text--black">{{  toFixedTwo(availableToDeposit / 1e18) }}</div>
              </div>
              <input placeholder="Placeholder" class="deposit__input" v-model="amount" type="number">
              <div class="deposit__row">
                <div class="deposit__item">
                  <button class="button button--yellow button--small" @click="maxOut">MAX</button>
                </div>
                <div class="deposit__item">
                  <div class="deposit__icons">
                    <div class="deposit__icon">
                      <img src="../assets/images/r.png" alt="">
                    </div>
                    <div class="deposit__icon">
                      <img src="../assets/images/eph.png" alt="">
                    </div>
                  </div>
                  ROOBEE-ETH LPs
                </div>
              </div>
              <!-- <div class="deposit__range">
                <div class="deposit__text">Weekly Rewards</div>
                <div class="deposit__text deposit__text--black">0 ROOBEE / week</div>
              </div> -->
            </div>
          </div>
          <div class="modal__cancel">
            <button class="button button--yellow button--small" @click="closeModal">Deposit</button>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import {mapActions, mapState} from 'vuex';
import toFixedTwo from '@/utils/toFixedTwo'

export default {
  name: "DepositModal",

  data() {
    return {
      show: false,
      amount: ''
    }
  },

  computed: {
    ...mapState(['availableToDeposit'])
  },

  methods: {
    ...mapActions(['deposit']),

    closeModal() {
      this.deposit(this.amount);
      this.show = false
    },

    maxOut() {
      this.amount = this.availableToDeposit / 1e18;
    },

    toFixedTwo(num) {
      return toFixedTwo(num)
    }
  }
}
</script>

<style scoped>

</style>