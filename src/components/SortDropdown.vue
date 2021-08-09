<template>
  <ElDropdown class="dropdown">
    <ElButton type="info">
      Sort the Budget List
      <i class="el-icon-arrow-down el-icon--right" />
    </ElButton>
    <ElDropdownMenu slot="dropdown">
      <ElDropdownItem>
        <p
          class="income"
          @click="sortList($event)"
        >
          Show only INCOME
        </p>
      </ElDropdownItem>
      <ElDropdownItem>
        <p
          class="outcome"
          @click="sortList($event)"
        >
          Show only OUTCOME
        </p>
      </ElDropdownItem>
      <ElDropdownItem>
        <p
          class="all"
          @click="sortList($event)"
        >
          Show all
        </p>
      </ElDropdownItem>
    </ElDropdownMenu>
  </ElDropdown>
</template>

<script>
export default {
  name: 'BudgetList',
  methods: {
    sortList({ target }) {
      this.$emit('sortList', target.classList);
    },
  },
};
</script>

<style scoped>
.dropdown {
  margin-bottom: 10px;
  margin-left: 300px;
}
p {
  margin: 0;
}
</style>
