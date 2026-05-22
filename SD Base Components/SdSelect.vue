<template>
  <a-select v-bind="$attrs" class="sd-select">
    <template v-for="(_, name) in $slots" #[name]="slotProps">
      <slot :name="name" v-bind="slotProps || {}"></slot>
    </template>
  </a-select>
</template>

<script setup lang="ts">
import { defineOptions } from 'vue';
defineOptions({ name: 'SdSelect' });
</script>

<style lang="less">
/* 去掉 scoped 且去掉 :deep，确保样式生效且不会成为无效选择器 */
.sd-select {
  background: transparent !important;

  .ant-select-selector {
    height: 32px !important;
    border-radius: 2px !important;
    align-items: center;
    background: #FFFFFF !important;
    background-color: #FFFFFF !important;
    font-size: 12px !important;
    color: var(--color-graphite-d40, #1F2329) !important;
  }
  
  .ant-select-selection-item {
    line-height: 30px !important;
    font-size: 12px !important;
    background: transparent !important;
    background-color: transparent !important;
  }
  
  .ant-select-selection-placeholder {
    line-height: 30px !important;
    font-size: 12px !important;
    color: var(--color-graphite, #A1A7B3) !important;
    background: transparent !important;
  }
}
</style>
