<template>
  <a-row align="center" :wrap="false">
    <a-col flex="auto">
      <a-menu
        mode="horizontal"
        :selected-keys="selectedKeys"
        @menu-item-click="doMenuClick"
      >
        <a-menu-item
          key="0"
          :style="{ padding: 0, marginRight: '38px' }"
          disabled
        >
          <div class="title-bar">
            <img class="logo" src="../assets/OIP-C.jpg" alt="logo" />
            <div class="title">NOJ</div>
          </div>
        </a-menu-item>
        <a-menu-item v-for="item in visibleRoutes" :key="item.path">
          {{ item.name }}
        </a-menu-item>
      </a-menu>
    </a-col>
    <a-col flex="100px">
      <div>
        <a-dropdown @select="handleSelect" trigger="hover">
          <a-button
            >{{ store.state.user?.loginUser?.userName ?? "未登录" }}
          </a-button>
          <template #content>
            <a-doption :value="'logout'">退出登录</a-doption>
            <!--                        <a-doption :value="{ value: 'Option3' }">Option 3</a-doption>-->
          </template>
        </a-dropdown>
      </div>
    </a-col>
  </a-row>
</template>

<script setup lang="ts">
import { routes } from "@/router/routes";
import { useRoute, useRouter } from "vue-router";
import { computed, ref } from "vue";
import { useStore } from "vuex";
import checkAccess from "@/access/checkAccess";
import ACCESS_ENUM from "@/access/accessEnum";
import { UserControllerService } from "@/generated";

const router = useRouter();
const route = useRoute();
const store = useStore();

const loginUser = store.state.user.loginUser;

// 展示在菜单的路由
const visibleRoutes = computed(() => {
  return routes.filter((item, index) => {
    // 过滤需要隐藏的菜单
    if (item.meta?.hideInMenu) {
      return false;
    }
    // todo 过滤没有权限的菜单
    if (!checkAccess(store.state.user.loginUser, item.meta?.access as string)) {
      return false;
    }

    return true;
  });
});

//默认主页
const selectedKeys = ref(["/"]);

// 路由跳转后，更新选中的菜单项
router.afterEach((to, from, failure) => {
  selectedKeys.value = [to.path];
});

const doMenuClick = (key: string) => {
  router.push(key);
};

/**
 * 处理下拉菜单的点击事件
 * @param v
 */
const handleSelect = (v: string) => {
  if (v === "logout") {
    logout();
  }
};

/**
 * 退出登录
 */
const logout = () => {
  console.log("退出登录");
  UserControllerService.userLogoutUsingPost();
  router.replace("/user/login");
};

// setTimeout(() => {
//   store.dispatch("user/getLoginUser", {
//     userName: "年年",
//     userRole: ACCESS_ENUM.ADMIN,
//   });
// }, 3000);
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.title-bar {
  display: flex;
  align-items: center;
}

.logo {
  height: 48px;
}

.title {
  color: #444;
  margin-left: 16px;
}

.arco-dropdown-open .arco-icon-down {
  transform: rotate(180deg);
}
</style>
