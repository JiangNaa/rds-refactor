<template>
  <div :class="getWrapClass">
    <LayoutBreadcrumb :theme="getHeaderTheme" />
  </div>
</template>
<script lang="ts">

  import { defineComponent, computed } from 'vue';

  import { Tabs } from 'ant-design-vue';

  import { initAffixTabs, useTabsDrag } from './useMultipleTabs';
  import LayoutBreadcrumb from './components/Breadcrumb.vue';
  import { useHeaderSetting } from '/@/hooks/setting/useHeaderSetting';
  import { useDesign } from '/@/hooks/web/useDesign';
  import { useMultipleTabSetting } from '/@/hooks/setting/useMultipleTabSetting';


  export default defineComponent({
    name: 'MultipleTabs',
    components: {
      Tabs,
      LayoutBreadcrumb,
      TabPane: Tabs.TabPane,
    },
    setup() {
      const {
        getHeaderTheme
      } = useHeaderSetting();
      const affixTextList = initAffixTabs();
      useTabsDrag(affixTextList);

      const { prefixCls } = useDesign('multiple-tabs');
      const { getShowQuick, getShowRedo, getShowFold } = useMultipleTabSetting();


      const getWrapClass = computed(() => {
        return [
          prefixCls
        ];
      });

      return {
        prefixCls,
        getHeaderTheme,
        getWrapClass,
        getShowQuick,
        getShowRedo,
        getShowFold,
      };
    },
  });
</script>
<style lang="less">
  @import './index.less';
</style>
