<template>
  <div>
    <h1>Hello! {{ playerName }} $ {{ yourMoney }}</h1>
    <div class="map">
      <div v-for="(item, index) in places" :key="index">
        <MapBox :data="item" :buy="handleBuy" />
      </div>
    </div>
  </div>
</template>

<script>
import MapBox from '../components/MapBox/';

export default {
  name: 'Main',
  components: {
    MapBox,
  },
  data() {
    return {
      yourMoney: 100000,
      places: [
        {
          name: 'New York',
          price: 3000,
        },
        {
          name: 'Taipei',
          price: 1000,
        },
        {
          name: 'Tokyo',
          price: 1500,
        },
        {
          name: 'Osaka',
          price: 1300,
        },
      ],
      playerName: 'Jico',
    };
  },
  methods: {
    handleBuy() {
      this.yourMoney -= 1000;
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
