<template>
  <ul class="list-group" style="width: 100%; background-color: #fefefe">
    <div
      class="col"
      v-for="accountItem in monthlyAccountList"
      :key="accountItem.id"
    >
      <AccountItem :accountItem="accountItem"></AccountItem>
    </div>
  </ul>
</template>

<script setup>
import { computed, onMounted } from 'vue';
import AccountItem from '@/components/AccountItem.vue';
import { useMonthlyAccountStore } from '@/stores/monthlyAccount.js';

const monthlyAccountListStore = useMonthlyAccountStore();
const { fetchMonthlyAccountList } = monthlyAccountListStore;

// 데이터 가져오기
onMounted(async () => {
  await fetchMonthlyAccountList(new Date().getMonth() + 1);
});

const monthlyAccountList = computed(
  () => monthlyAccountListStore.monthlyAccountList
);

// 데이터 변경 감지하여 업데이트
</script>

<style scoped>
.list-group-item {
  margin-bottom: 1em;
}
</style>
