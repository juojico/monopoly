<template>
  <div
    :class="'mapBox ' + position||''"
    :style="'border-color: rgba(' + bgc + ');'"
    @click="handleClick(data.price)"
  >
    <div class="mapBoxName">
      {{ data.name }}
    </div>
    <div class="mapBoxPrice">$ {{ data.price }}</div>
    <div class="mapBoxOwer">{{ ower ? ower + '擁有' : '尚未擁有者' }}</div>
    Lv {{ level }}
  </div>
</template>

<script>
export default {
  name: 'MapBox',
  props: {
    data: Object,
    buy: Function,
    currentPlayer: String,
    position: String,
  },
  data() {
    return {
      level: 0,
      ower: '',
    };
  },
  methods: {
    handleClick(price) {
      console.log(this.ower, this.currentPlayer);
      if (this.ower === this.currentPlayer || this.ower === '') {
        this.ower = this.currentPlayer;
        this.buy(price);
        this.level++;
      }
    },
  },
  computed: {
    bgc: function () {
      const randomV = (num) => Math.round(Math.random() * num);
      const newColor = [randomV(250), randomV(160), randomV(25)];
      return newColor;
    },
  },
};
</script>

<style lang="scss">
.mapBox {
  min-width: 150px;
  height: 150px;
  padding: 10px;
  background-color: #fefefe;
  border: 10px solid #333;
  border-top-width: 50px;
  color: #333;
  outline: 4px solid #333;
  cursor: pointer;
  user-select: none;

  &.left {
    height: 100px;
    border-top-width: 10px;
    border-left-width: 50px;
  }

  &.right {
    height: 100px;
    border-top-width: 10px;
    border-right-width: 50px;
  }

  &Name {
    font-size: 24px;
  }
  &Price {
    font-size: 16px;
  }
}
</style>
