<template>
  <div class="container" v-if="tokenInfo.token">
    <div class="item" @click.prevent="handleClick()">
      <div class="left">
        <img v-bind:src="require('../assets/' + tokenInfo.token + '.png')" :alt="tokenInfo.token" />
        <div class="token">
          <div>{{ parseToken() }}</div>
          <div>{{ tokenInfo.from }}</div>
        </div>
      </div>
      <div class="right">
        <div class="price">
          <div>{{ tokenInfo.price }}</div>
          <div>{{ parseDateTime() }}</div>
        </div>
        <div class="change">{{ tokenInfo.change }}</div>
      </div>
    </div>
    <div class="separator" />
  </div>
  <div v-else>{{ tokenInfo }}</div>
</template>

<script>
import { parseTime } from '../utils/index'
export default {
  name: 'TokenPrice',
  props: ['tokenInfo'],
  methods: {
    handleClick: function() {
      this.$router.push(`/history/${this.tokenInfo.token}`)
    },

    parseToken: function() {
      return `${this.tokenInfo.token.toUpperCase()}/USDT`
    },

    parseDateTime: function() {
      return parseTime(this.tokenInfo.timestamp)
    },
  },
}
</script>

<style lang="scss" scoped>
.container {
  padding: 8px 16px;
}

.item {
  display: flex;
  justify-content: space-between;
  padding-bottom: 8px;
}

.left {
  display: flex;
  flex: 1.2;
}

.right {
  display: flex;
  flex: 1;
  justify-content: space-between;
}

.token {
  margin-left: 12px;

  div:first-child {
    font-size: 18px;
    font-weight: 600;
  }

  div:last-child {
    margin-top: 5px;
    font-size: 14px;
    text-align: left;
  }
}

.price {
  div:first-child {
    font-size: 18px;
    font-weight: 600;
    text-align: left;
  }

  div:last-child {
    margin-top: 5px;
    font-size: 14px;
    text-align: left;
  }
}

.change {
  margin-left: 12px;
  font-size: 16px;
  background: red;
  color: white;
  height: 30px;
  line-height: 30px;
  font-weight: 600;
  min-width: 80px;
  text-align: center;
  border-radius: 6px;
}

img {
  width: 28px;
  height: 28px;
}

.separator {
  background: #ececec;
  width: 100%;
  height: 1px;
}
</style>
