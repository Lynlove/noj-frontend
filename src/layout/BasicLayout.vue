<script setup lang="ts">
import GlobalHeader from "@/components/GlobalHeader.vue";
</script>

<template>
  <div id="basicLayout">
    <a-layout class="header" style="min-height: 100vh">
      <a-layout-header>
        <GlobalHeader />
      </a-layout-header>
      <a-layout-content class="content">
        <router-view />
      </a-layout-content>
      <a-layout-footer class="footer">
        <a-space>
          <a class="link" href="https://github.com/Lynlove" target="_blank">
            <icon-github />
            年年的GitHub</a
          >
          <a class="link" href="https://beian.miit.gov.cn/" target="_blank"
            >湘ICP备2024072430号-1</a
          >
          <a
            class="link"
            href="https://beian.mps.gov.cn/#/query/webSearch"
            target="_blank"
            >湘公网安备43090002000102号</a
          >
        </a-space>
      </a-layout-footer>
    </a-layout>
  </div>
</template>

<style scoped>
.link {
  text-decoration: none;
}

#basicLayout {
}

#basicLayout .header {
  box-shadow: #eee 1px 1px 5px;
}

#basicLayout .content {
  background: linear-gradient(to right, #fefefe, #fff);
  margin-bottom: 16px;
  padding: 20px;
}

#basicLayout .footer {
  background: #efefef;
  padding: 16px;
  position: sticky;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
}
</style>
