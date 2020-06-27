<template>
  <div
    class="mapBox"
    :style="'background-color: rgba(' + bgc + ');'"
    @click="handleClick()"
  >
    <div class="mapBoxName">
      {{ data.name }}
    </div>
    <div class="mapBoxPrice">$ {{ data.price }}</div>
    {{ level }}
  </div>
</template>

<script>
export default {
  name: 'MapBox',
  props: { data: Object, buy: Function },
  data() {
    return {
      level: 1,
    };
  },
  methods: {
    handleClick() {
      this.buy();
      this.level++;
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
  width: 150px;
  height: 150px;
  padding: 10px;
  background-color: #369;
  color: white;
  cursor: pointer;
  user-select: none;
  &Name {
    font-size: 24px;
  }
  &Price {
    font-size: 16px;
  }
}
</style>
