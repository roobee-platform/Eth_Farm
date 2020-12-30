<template>
    <div class="index-page">
      <div class="info">
        <div class="container">
          <div class="info__image">
             <img src="../assets/images/cat.png" alt="">
          </div>
          <div class="title">Roobee Farm</div>
          <div class="balance">
            <div class="balance__inner">
              <div class="balance__item">
                <div class="balance__title">Your Roobee Balance</div>
                <div class="balance__amount">
                  {{ toFixedTwo(roobeeBalance / 1e18) }}
                </div>
                <div class="balance__total">
                  <div class="balance__total-name">Reward Per Token</div>
                  <div class="balance__total-cost">{{ toFixedTwo(rewardPerToken / 1e18) }} ROOBEE</div>
                </div>
              </div>
              <div class="balance__item balance__item--farm">
                <div class="balance__title">Farming is over.<br>Stay tuned!</div>
              </div>
            </div>
            <div class="balance__info">
              <div class="balance__icon">!</div>
              <div class="balance__name">Pro Tip</div> - Add your Uniswap ROOBEE-ETH LPs liquidity provider tokens to farm ROOBEE
            </div>
            <div class="balance__button">
              <router-link :to="{name: 'farming'}" class="button button--yellow button--small">Start Farming</router-link>
            </div>

          </div>
        </div>
      </div>

    </div>
</template>

<script>
import moment from 'moment';
import {mapState, mapActions} from 'vuex';
import toFixedTwo from '@/utils/toFixedTwo'

export default {
  name: 'Home',

  data() {
    return {
      finishPeriodInterval: null,
      timeLeft: 0
    }
  },

  created() {
    if (!this.firstEnter) {
      this.getRoobeeData();
    }

    // this.startFinishPeriodTimer();
  },

  watch: {
    finishPeriod() {
      // this.startFinishPeriodTimer();
    }
  },

  computed: {
    ...mapState(['roobeeBalance', 'rewardPerToken', 'finishPeriod', 'rewardPerBlock', 'firstEnter'])
  },

  methods: {
    ...mapActions(['getRoobeeData']),

    startFinishPeriodTimer() {
      if (this.finishPeriodInterval)
        clearInterval(this.finishPeriodInterval);
      if (this.finishPeriod > 0) {
        this.finishPeriodInterval = setInterval(() => {
          let delta = this.finishPeriod - moment().unix();
          const days = Math.floor(delta / 86400);
          delta -= days * 86400;
          const hours = Math.floor(delta / 3600) % 24;
          delta -= hours * 3600;
          const minutes = Math.floor(delta / 60) % 60;
          delta -= minutes * 60;
          const seconds = delta % 60;
          this.timeLeft = `${days < 10 ? `0${days}` : days}:${hours < 10 ? `0${hours}` : hours}:${minutes < 10 ? `0${minutes}` : minutes}:${seconds < 10 ? `0${seconds}` : seconds}`;
        }, 1000);
      }
    },

    toFixedTwo(num) {
      return toFixedTwo(num)
    }
  }
}
</script>
