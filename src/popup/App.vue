<template>
  <div class="container">
    <el-tabs v-model="currentTab" class="gitlab-tabs" @tab-click="onTabClick">
      <el-tab-pane label="To Review" name="to_review">
        <template #label>
          To Review <span class="badge">{{ toReviewCount }}</span>
        </template>
      </el-tab-pane>
      <el-tab-pane label="Under Review" name="under_review">
        <template #label>
          Under Review <span class="badge">{{ underReviewCount }}</span>
        </template>
      </el-tab-pane>
      <el-tab-pane label="Drafts" name="drafts"></el-tab-pane>
      <el-tab-pane label="Issues" name="issues">
        <template #label>
          Issues <span class="badge">{{ issuesCount }}</span>
        </template>
      </el-tab-pane>
      <el-tab-pane label="To-Do List" name="todo_list">
        <template #label>
          To-Do List <span class="badge">{{ todoListCount }}</span>
        </template>
      </el-tab-pane>
    </el-tabs>

    <main class="content">
      <div class="error-message" v-if="currentTab === 'to_review'">
        <p>Failed to fetch</p>
        <a href="#">Details</a>
      </div>
      <component :is="currentTabComponent"></component>
    </main>

    <footer class="footer">
      <el-button class="refresh" type="primary" @click="refreshData">Refresh</el-button>
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import type { TabsPaneContext } from 'element-plus'
import ToReviewComponent from './components/ToReviewComponent.vue';
import UnderReviewComponent from './components/UnderReviewComponent.vue';
import DraftsComponent from './components/DraftsComponent.vue';
import IssuesComponent from './components/IssuesComponent.vue';
import TodoListComponent from './components/TodoListComponent.vue';


const currentTab = ref('to_review');
const toReviewCount = ref(0);
const underReviewCount = ref(2);
const issuesCount = ref(0);
const todoListCount = ref(0);

const currentTabComponent = computed(() => {
  switch (currentTab.value) {
    case 'to_review':
      return ToReviewComponent;
    case 'under_review':
      return UnderReviewComponent;
    case 'drafts':
      return DraftsComponent;
    case 'issues':
      return IssuesComponent;
    case 'todo_list':
      return TodoListComponent;
    default:
      return null;
  }
});

const refreshData = () => {
  console.log('Data refreshed');
};

const onTabClick = (tab: TabsPaneContext) => {
  console.log('Selected Tab:', tab);
};
</script>


<style>
.gitlab-tabs > .el-tabs__content {
  padding: 32px;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
}
</style>