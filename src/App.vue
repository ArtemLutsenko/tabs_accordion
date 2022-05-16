<template>
  <div class="container">
    <t-tabs />
  </div>
</template>

<script>
import TTabs from '@/components/Tabs.vue';

export default {
  name: 'App',
  components: {
    TTabs,
  },
};
</script>

<style lang="scss">
.container {
  font-family: Open-Sans, sans-serif;
  display: flex;
  justify-content: center;
  height: 96vh;
  padding-top: 10px;
  box-sizing: border-box;

  @media (max-width: 756px) {
    padding: 0;
    justify-content: left;
  }
}
</style>
