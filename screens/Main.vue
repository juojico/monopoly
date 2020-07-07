<template>
  <div>
    <h1>
      輪到
      <span :style="'color: ' + players[currentPlayer].color + ';'">{{
        players[currentPlayer].name
      }}</span>
      了 $
      {{ players[currentPlayer].money }}
    </h1>
    <div class="map">
      <div class="block"></div>
      <div class="block">
        <MapBox
          v-for="(item, index) in places.taiwan"
          :key="index"
          :data="item"
          :buy="handleBuy"
          :currentPlayer="players[currentPlayer].name"
        />
      </div>
      <div class="block"></div>

      <div class="block vertical">
        <MapBox
          v-for="(item, index) in places.usa"
          :key="index"
          :data="item"
          :buy="handleBuy"
          :currentPlayer="players[currentPlayer].name"
          position="left"
        />
      </div>
      <div class="block">
        <div class="playBlock">
          <Dice :value="diceValue" :rolled="rolled" />
          <BtnGo :onclick="rollDice" :disabled="btnGoOff" />
          <div>{{ diceValue }}</div>
        </div>
      </div>
      <div class="block vertical">
        <MapBox
          v-for="(item, index) in places.japan"
          :key="index"
          :data="item"
          :buy="handleBuy"
          :currentPlayer="players[currentPlayer].name"
          position="right"
        />
      </div>

      <div class="block"></div>
      <div class="block">
        <MapBox
          v-for="(item, index) in places.seasia"
          :key="index"
          :data="item"
          :buy="handleBuy"
          :currentPlayer="players[currentPlayer].name"
        />
      </div>
      <div class="block"></div>
    </div>

    <Chess :style="'left: ' + diceValue * 10 + '%'" />

    <div>
      <div v-for="(item, index) in players" :key="index">
        {{ item.name + item.money }}
      </div>
    </div>
  </div>
</template>

<script>
import MapBox from '../components/MapBox/';
import BtnGo from '../components/Button/BtnGo';
import Dice from '../components/Dice';
import Chess from '../components/Characters/Chess';
import { PLACES } from '../constants/map';

export default {
  name: 'Main',
  components: {
    MapBox,
    BtnGo,
    Dice,
    Chess,
  },
  data() {
    return {
      places: PLACES,
      currentPlayer: 0,
      yourName: '',
      diceValue: 1,
      rolled: 0,
      btnGoOff: false,
      players: [
        { name: 'Doris', money: 10000, color: '#f8c' },
        { name: 'Emma', money: 8000, color: '#39a' },
        { name: 'Lara', money: 12000, color: '#94f' },
        { name: 'Mia', money: 15000, color: '#29d' },
      ],
    };
  },
  methods: {
    handleBuy(price) {
      this.players[this.currentPlayer].money -= price;
      this.nextTurn();
    },
    nextTurn() {
      this.currentPlayer++;
      if (this.currentPlayer > 3) {
        this.currentPlayer = 0;
      }
    },
    rollDice() {
      this.rolled++;
      this.btnGoOff = true;
      setTimeout(() => {
        this.btnGoOff = false;
      }, 1000);
      const diceVal = Math.round(Math.random() * 5) + 1;
      this.diceValue = diceVal;
    },
  },
};
</script>

<style lang="scss">
.map {
  display: grid;
  grid-template-columns: auto auto auto;
  background-color: #eee;

  .block {
    display: flex;
    justify-content: center;
    align-items: stretch;

    &.vertical {
      flex-direction: column;
    }
  }
}

.playBlock {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-direction: column;
}
</style>
