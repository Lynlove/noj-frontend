<script setup lang="ts"></script>

<template>
  <div id="userLayout">
    <a-layout class="header" style="min-height: 100vh">
      <a-layout-header style="margin-top: 30px">
        <a-space>
          <img src="@/assets/OIP-C.jpg" class="logo" alt="logo" />
          <div>NOJ</div>
        </a-space>
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

#userLayout {
  text-align: center;
  background: url("https://gw.alipayobjects.com/zos/rmsportal/FfdJeJRQWjEeGTpqgBKj.png")
    0% 0% / 100% 100%;
}

#userLayout .logo {
  width: 64px;
  height: 64px;
}

#userLayout .header {
}

#userLayout .content {
  margin-bottom: 16px;
  padding: 20px;
}

#userLayout .footer {
  padding: 16px;
  position: sticky;
  bottom: 0;
  left: 0;
  right: 0;
  text-align: center;
}
</style>
