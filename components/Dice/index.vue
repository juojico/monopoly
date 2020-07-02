<template>
  <div class="dice">
    <div :class="'diceFace dice1 ' + diceFaces[0]">
      1
    </div>
    <div :class="'diceFace dice2 ' + diceFaces[1]">
      2
    </div>
    <div :class="'diceFace dice3 ' + diceFaces[2]">
      3
    </div>
    <div :class="'diceFace dice4 ' + diceFaces[3]">
      4
    </div>
    <div :class="'diceFace dice5 ' + diceFaces[4]">
      5
    </div>
    <div :class="'diceFace dice6 ' + diceFaces[5]">
      6
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dice',
  props: { value: Number },
  data() {
    return {
      diceFaces: ['front', 'up', 'left', 'right', 'bottom', 'back'],
    };
  },
  watch: {
    value: function () {
      console.log('this.diceFaces', this.diceFaces);
      return this.diceFaces.sort(() => 0.5 - Math.random());
    },
  },
};
</script>

<style lang="scss">
@keyframes rotateDice {
  0% {
    perspective-origin: 100%;
  }
  50% {
    perspective-origin: -100%;
  }
  100% {
    transform: rotate(360deg);
    perspective-origin: 100%;
  }
}

.dice {
  position: relative;
  width: 100px;
  height: 100px;
  perspective: 500px;
  perspective-origin: -100% -100%;
//   animation: rotateDice 2s infinite linear;

  &Face {
    position: absolute;
    width: 100px;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #fefefe;
    border-radius: 12px;
    font-size: 40px;
    transition: 1s;
  }

  .front {
    transform: translateZ(50px);
    background-color: #f9f9f9;
    z-index: 6;
  }
  .back {
    transform: translateZ(-50px);
    z-index: 1;
  }
  .up {
    transform: rotateX(90deg) translateZ(50px);
    z-index: 4;
  }
  .bottom {
    transform: rotateX(-90deg) translateZ(50px);
    background-color: #eee;
    z-index: 2;
  }
  .right {
    transform: rotateY(90deg) translateZ(50px);
    background-color: #f3f3f3;
    z-index: 3;
  }
  .left {
    transform: rotateY(-90deg) translateZ(50px);
    background-color: #f3f3f3;
    z-index: 3;
  }
}
</style>
