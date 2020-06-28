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
      <div v-for="(item, index) in places" :key="index">
        <MapBox
          :data="item"
          :buy="handleBuy"
          :currentPlayer="players[currentPlayer].name"
        />
      </div>
    </div>

    <div>
      <div v-for="(item, index) in players" :key="index">
        {{ item.name + item.money }}
      </div>
    </div>
  </div>
</template>

<script>
import MapBox from '../components/MapBox/';
import { PLACES } from '../constants/map';

export default {
  name: 'Main',
  components: {
    MapBox,
  },
  data() {
    return {
      places: PLACES,
      currentPlayer: 0,
      yourName: '',
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
  },
};
</script>

<style>
.map {
  width: 800px;
  height: 500px;
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
}
</style>
