<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" id="logo">
    <div class="action-area">
      <button
        class="btn"
        v-for="amount in amountList"
        :key="amount"
        @click="createPayment(amount)"
      >{{amount}} LOBI</button>
    </div>
  </div>
</template>

<script>
import coinview from '@coinjinja/coinview-sdk'

export default {
  name: 'app',
  data() {
    return {
      amountList: [1, 2, 3, 4],
      app: null,
    }
  },
  mounted() {
    coinview
      .init('knqXAPaw', true, '192.168.2.144:9000')
      .then(() => coinview.user.assets())
      .then(assets => coinview.log('ASSETS', assets))
  },
  methods: {
    createPayment(amount) {
      coinview.payment.create({
        assetId: 'd0deee89-a0f3-34ec-a92c-1a4d16fd2c3d',
        amount,
        memo: 'Payment Test',
        description: `Test Payment ${amount} LOBI`,
      })
    },
  },
}
</script>

<style>
#app {
  width: 100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  position: relative;
}
#logo {
  width: 100%;
}
.action-area {
  flex: 1;
  padding: 16px;
}
.btn {
  width: 100%;
  height: 48px;
  background: #666;
  border: none;
  color: white;
  font-size: 24px;
  margin-bottom: 24px;
}
</style>
