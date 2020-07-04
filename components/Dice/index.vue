<template>
  <div class="diceWrap">
    <div :class="diceClass">
      <div class="diceFace front"></div>
      <div class="diceFace up"></div>
      <div class="diceFace left"></div>
      <div class="diceFace right"></div>
      <div class="diceFace bottom"></div>
      <div class="diceFace back"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dice',
  props: { value: Number, rolled: Number },
  data() {
    return {
      diceClass: 'dice',
    };
  },
  methods: {
    onRolls() {
      this.onRoll();
      console.log('onRoll');
    },
  },
  watch: {
    rolled: function () {
      this.diceClass = 'dice throw value' + this.value;
      setTimeout(() => {
        this.diceClass = 'dice value' + this.value;
      }, 1000);
    },
  },
};
</script>

<style lang="scss">
$diceBg: #f6f3f0;
$diceColor1: #f63330 !default;
$diceColor2: #131210 !default;
$diceRadius: 20px !default;

$redDice: false !default;
$blueDice: false !default;
$blackDice: false !default;
$pinkDice: false !default;

@if $redDice {
  $diceBg: rgba(250, 0, 0, 0.45);
  $diceColor1: white;
  $diceColor2: white;
  $diceRadius: 30px;
}

@if $blueDice {
  $diceBg: rgba(0, 0, 255, 0.45);
  $diceColor1: white;
  $diceColor2: white;
}

@if $blackDice {
  $diceBg: #111;
  $diceColor1: #3ef;
  $diceColor2: #db0;
}

@if $pinkDice {
  $diceBg: #f69;
  $diceColor1: #fe9;
  $diceColor2: #ffe;
  $diceRadius: 40px;
}

@keyframes rotateDice {
  30% {
    transform: rotate3d(1, 1, 1, 0deg);
  }
  100% {
    transform: rotate3d(1, 1, 1, 720deg);
  }
}

@keyframes rotatePerFace {
  16% {
    transform: rotate3d(-0.1, 0.6, -0.4, 180deg);
  }
  32% {
    transform: rotate3d(-0.85, -0.42, 0.73, 180deg);
  }
  48% {
    transform: rotate3d(-0.8, 0.3, -0.75, 180deg);
  }
  64% {
    transform: rotate3d(0.3, 0.45, 0.9, 180deg);
  }
  80% {
    transform: rotate3d(-0.16, 0.6, 0.18, 180deg);
  }
  100% {
    transform: rotate3d(-0.1, 0.3, -1, 180deg);
  }
}

@keyframes throwDice {
  20% {
    margin-top: -100px;
  }
  40% {
    margin-top: 0px;
  }
  60% {
    margin-top: -30px;
  }
  80% {
    margin-top: 0px;
  }
  85% {
    margin-top: -10px;
  }
  90% {
    margin-top: 0px;
  }
  95% {
    margin-top: -3px;
  }
  100% {
    margin-top: 0px;
  }
}

.diceWrap {
  position: relative;
  width: 200px;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;

  &::before {
    position: absolute;
    content: '';
    width: 70%;
    height: 70%;
    top: 40%;
    left: 10%;
    background: rgba(0, 0, 0, 0.05);
    border-radius: 100%;
    filter: blur(10px);
  }
}

.dice {
  width: 100px;
  height: 100px;
  transform-style: preserve-3d;
  transform: rotate3d(0, 0.9, 0.9, 90deg);
  transition: 0.5s cubic-bezier(0.42, 1.57, 0.62, 0.86);

  &.rolling {
    animation: rotatePerFace 3s cubic-bezier(0.42, 1.57, 0.62, 0.86) infinite;
  }

  &.throw {
    animation: rotateDice 0.7s ease-in reverse, throwDice 1s linear;
  }

  &.value1 {
    transform: rotate3d(-0.1, 0.3, -1, 180deg);
  }

  &.value2 {
    transform: rotate3d(-0.1, 0.6, -0.4, 180deg);
  }

  &.value3 {
    transform: rotate3d(-0.85, -0.42, 0.73, 180deg);
  }

  &.value4 {
    transform: rotate3d(-0.8, 0.3, -0.75, 180deg);
  }

  &.value5 {
    transform: rotate3d(0.3, 0.45, 0.9, 180deg);
  }

  &.value6 {
    transform: rotate3d(-0.16, 0.6, 0.18, 180deg);
  }

  &Face {
    box-sizing: border-box;
    position: absolute;
    width: 100px;
    height: 100px;
    background-color: $diceBg;
    border: 2px solid lighten($diceBg, 10%);
    border-radius: $diceRadius;
    transform-style: preserve-3d;

    &::before {
      position: absolute;
      content: '';
      width: 100%;
      height: 100%;
      background-color: lighten($diceBg, 10%);
      border-radius: 20px;
      transform: translateZ(-1px);
    }

    &::after {
      position: absolute;
      content: '';
      width: 20px;
      height: 20px;
      top: 50%;
      left: 50%;
      margin: -10px 0 0 -10px;
      background-color: $diceColor2;
      border-radius: 100%;
      transform: translateZ(1px);
    }
  }

  .front {
    transform: translateZ(50px);
    &::after {
      width: 40px;
      height: 40px;
      margin: -20px 0 0 -20px;
      background-color: $diceColor1;
    }
  }

  .up {
    transform: rotateX(90deg) translateZ(50px);
    &::after {
      margin: -30px 0 0 -30px;
      box-shadow: 40px 40px $diceColor2;
    }
  }

  .left {
    transform: rotateY(-90deg) translateZ(50px);
    &::after {
      margin: -40px 0 0 -40px;
      box-shadow: 30px 30px $diceColor2, 60px 60px $diceColor2;
    }
  }

  .right {
    transform: rotateY(90deg) translateZ(50px);
    &::after {
      margin: -30px 0 0 -30px;
      background-color: $diceColor1;
      box-shadow: 40px 0px $diceColor1, 0px 40px $diceColor1,
        40px 40px $diceColor1;
    }
  }

  .bottom {
    transform: rotateX(-90deg) translateZ(50px);
    &::after {
      margin: -36px 0 0 -36px;
      box-shadow: 26px 26px $diceColor2, 52px 52px $diceColor2,
        52px 0px $diceColor2, 0px 52px $diceColor2;
    }
  }

  .back {
    transform: rotateX(180deg) translateZ(50px);
    &::after {
      margin: -40px 0 0 -30px;
      box-shadow: 40px 0px $diceColor2, 0px 30px $diceColor2,
        40px 30px $diceColor2, 0px 60px $diceColor2, 40px 60px $diceColor2;
    }
  }
}
</style>
