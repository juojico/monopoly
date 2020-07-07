<template>
  <div :class="role ? 'chess ' + role : 'chess'"></div>
</template>

<script>
export default {
  name: 'Chess',
  props: { role: String },
};
</script>

<style lang="scss">
.chess {
  position: absolute;
  width: 50px;
  height: 50px;
  top: 100px;
  left: 10%;
  border-radius: 100%;
  background-color: #ff2929;
  transition: 1s;

  user-select: none;
  &::before {
    position: absolute;
    content: '';
    top: 0;
    left: 0;
    border: 25px solid transparent;
    border-bottom: 75px solid #ff2929;
  }
}
</style>
