<template>
  <div :class="disabled ? 'btnGo disabled' : 'btnGo'" @click="onclick">GO!</div>
</template>

<script>
export default {
  name: 'BtnGo',
  props: { onclick: Function, disabled: Boolean },
};
</script>

<style lang="scss">
.btnGo {
  width: 100px;
  height: 100px;
  background-color: #ff2929;
  color: white;
  font-size: 32px;
  font-weight: bold;
  border-radius: 100%;
  line-height: 100px;
  text-align: center;
  box-shadow: 0 6px #672012, 0 6px 10px rgba(0, 0, 0, 0.2);
  transition: 0.1s;
  cursor: pointer;
  user-select: none;

  &.disabled {
    margin-top: 2px;
    background-color: #a03f3f;
    box-shadow: 0 4px #672012, 0 4px 10px rgba(0, 0, 0, 0.2);
    pointer-events: none;
  }
}
</style>
