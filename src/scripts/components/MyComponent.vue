<template>
    <div>{{ $props.message }}</div>
</template>

<script>
import VueTypes from 'vue-types';

export default {
  props: {
    message: VueTypes.arrayOf(VueTypes.shape({
      // id: VueTypes.number.isRequired,
      text1: VueTypes.string.isRequired,
      text2: VueTypes.string.isRequired
    })).isRequired
  }
};
</script>

<style lang="scss" scoped>
//
</style>
