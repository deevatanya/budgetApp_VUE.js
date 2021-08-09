<template>
  <div
    class="total-value"
    :style="{'color' :colorTotal}"
  >
    Balance: {{ total }}
  </div>
</template>

<script>
export default {
  name: 'Total',
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
  computed: {
    colorTotal() {
      let color = 'black';
      if (this.total > 0) {
        color = 'green';
      } else if (this.total < 0) {
        color = 'red';
      } else {
        color = 'black';
      }
      return color;
    },
  },
};
</script>

<style scoped>
.total-value {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
</style>
