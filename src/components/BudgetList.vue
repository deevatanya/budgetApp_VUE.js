<template>
  <div
    class="budget-list-wrap"
  >
    <SortDropdown @sortList="sortList" />
    <ElCard :header="header">
      <BudgetListItem
        v-if="!isEmpty"
        :list="list"
        @deleteItem="deleteItem"
        :income="sortIncome"
        :outcome="sortOutcome"
      />
      <ElAlert
        v-else
        type="info"
        :title="emptyTitle"
        :closable="false"
      />
    </ElCard>
  </div>
</template>

<script>
import BudgetListItem from '@/components/BudgetListItem.vue';
import SortDropdown from '@/components/SortDropdown.vue';

export default {
  name: 'BudgetList',
  components: {
    BudgetListItem,
    SortDropdown,
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
  },
  data: () => ({
    header: 'Budget List',
    emptyTitle: 'Empty List',
    sortIncome: false,
    sortOutcome: false,
  }),
  computed: {
    isEmpty() {
      return !Object.keys(this.list).length;
    },
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
    },
    sortList(classList) {
      // this.$emit('sortList', classList);

      if (classList.contains('income')) {
        this.sortOutcome = false;
        this.sortIncome = true;
      } else if (classList.contains('outcome')) {
        this.sortIncome = false;
        this.sortOutcome = true;
      } else {
        this.sortIncome = false;
        this.sortOutcome = false;
      }
    },
  },
};
</script>

<style scoped>
.budget-list-wrap {
  max-width: 500px;
  margin: auto;
}
</style>
