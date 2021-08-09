<template>
  <div>
    <div
      class="list-item"
      v-for="(item, index) in sortList"
      :key="index"
    >
      <i
        class="el-icon-top"
        v-if="item.type === 'INCOME'"
      />
      <i
        class="el-icon-bottom"
        v-else
      />
      <span class="budget-comment">{{ item.comment }}</span>
      <span class="budget-value">{{ item.value }}</span>
      <ElButton
        type="danger"
        size="mini"
        @click="dialogVisible = true"
      >
        Delete
      </ElButton>
      <ElDialog
        :visible.sync="dialogVisible"
        width="30%"
      >
        <span>Are you sure you want to delete "{{ item.comment }}" ?</span>
        <span
          slot="footer"
          class="dialog-footer"
        >
          <ElButton @click="dialogVisible = false">Cancel</ElButton>
          <ElButton
            type="primary"
            @click="deleteItem(item.id)"
          >
            Confirm
          </ElButton>
        </span>
      </ElDialog>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BudgetListItem',
  data() {
    return {
      dialogVisible: false,
    };
  },
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
    income: { type: Boolean },
    outcome: { type: Boolean },
  },
  methods: {
    deleteItem(id) {
      this.$emit('deleteItem', id);
      this.dialogVisible = false;
    },
  },
  computed: {
    sortList() {
      const list = Object.values(this.list);
      if (this.income) {
        return list.filter((item) => item.type === 'INCOME');
      }
      if (this.outcome) {
        return list.filter((item) => item.type === 'OUTCOME');
      }
      return list;
    },
  },
};
</script>

<style scoped>
.list-item {
  display: flex;
  text-align: center;
  padding: 10px 15px;
}
.budget-comment {
  margin-left: 10px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
</style>
