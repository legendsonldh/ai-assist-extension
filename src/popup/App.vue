<script setup lang="ts">
import { ref, computed } from 'vue';
import ToReviewComponent from './components/ToReviewComponent.vue';
import UnderReviewComponent from './components/UnderReviewComponent.vue';
import DraftsComponent from './components/DraftsComponent.vue';
import IssuesComponent from './components/IssuesComponent.vue';
import TodoListComponent from './components/TodoListComponent.vue';

// 假设的状态和方法
const currentTab = ref('to_review');
const toReviewCount = ref(0);
const underReviewCount = ref(2);
const issuesCount = ref(0);
const todoListCount = ref(0);

const setCurrentTab = (tab: string) => {
  currentTab.value = tab;
};

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
</script>

<template>
  <div class="container">
    <header class="header">
      <div class="tabs">
        <button :class="{ active: currentTab === 'to_review' }" @click="setCurrentTab('to_review')">To Review {{ toReviewCount }}</button>
        <button :class="{ active: currentTab === 'under_review' }" @click="setCurrentTab('under_review')">Under Review {{ underReviewCount }}</button>
        <button :class="{ active: currentTab === 'drafts' }" @click="setCurrentTab('drafts')">Drafts</button>
        <button :class="{ active: currentTab === 'issues' }" @click="setCurrentTab('issues')">Issues {{ issuesCount }}</button>
        <button :class="{ active: currentTab === 'todo_list' }" @click="setCurrentTab('todo_list')">To-Do List {{ todoListCount }}</button>
      </div>
    </header>
    <main>
      <!-- 根据 currentTab 显示不同的内容 -->
      <component :is="currentTabComponent"></component>
    </main>
    <footer>
      <!-- 页脚内容 -->
    </footer>
  </div>
</template>

<script setup lang="ts"></script>

<style scoped>
/* 头部样式 */
.header {
  background-color: #f8f9fa; /* 背景颜色 */
  padding: 10px 20px; /* 内边距 */
  border-bottom: 1px solid #dee2e6; /* 下边框 */
  display: flex; /* 使用 Flexbox 布局 */
  align-items: center; /* 垂直居中 */
  justify-content: space-between; /* 两端对齐 */
}

/* 标签页容器样式 */
.tabs {
  display: flex; /* 使用 Flexbox 布局 */
  gap: 10px; /* 标签之间的间隔 */
  list-style: none; /* 移除列表样式 */
  margin: 0; /* 移除外边距 */
  padding: 0; /* 移除外边距 */
}

/* 标签页按钮样式 */
.tabs button {
  background-color: #e9ecef; /* 背景颜色 */
  border: 1px solid #ced4da; /* 边框 */
  border-radius: 0.25rem; /* 圆角 */
  padding: 0.5rem 1rem; /* 内边距 */
  cursor: pointer; /* 鼠标悬停时显示指针 */
  transition: background-color 0.3s, color 0.3s; /* 平滑背景颜色和文字颜色变化 */
}

/* 活动标签页按钮样式 */
.tabs button.active {
  background-color: #007bff; /* 活动状态背景颜色 */
  color: white; /* 文字颜色 */
  border-color: #007bff; /* 边框颜色 */
}

/* 标签页按钮悬停效果 */
.tabs button:hover {
  background-color: #dee2e6; /* 悬停时背景颜色 */
}

/* 内容区域样式 */
#content {
  padding: 20px; /* 内边距 */
}
</style>