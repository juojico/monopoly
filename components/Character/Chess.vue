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
  width: 100px;
  height: 100px;
  background-color: #ff2929;
  user-select: none;
}
</style>
