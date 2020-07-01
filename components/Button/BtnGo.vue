<template>
  <div class="btnGo" @click="onclick">GO!</div>
</template>

<script>
export default {
  name: 'BtnGo',
  props: { onclick: Function },
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
  cursor: pointer;
  user-select: none;
}
</style>
