<template>
  <header class="header">
    <div class="header__logo">
      <AppLogo />
    </div>
    <div class="header__cart">
      <router-link
        to="/cart"
        data-test="link-cart"
        >{{ totalSum }} ₽</router-link
      >
    </div>

    <div
      v-if="!user"
      key="header-with-no-user"
      class="header__user"
    >
      <router-link
        to="/login"
        class="header__login"
        data-test="link-login"
      >
        <span>Войти</span>
      </router-link>
    </div>

    <div
      v-else
      key="header-with-user"
      class="header__user"
    >
      <router-link
        to="/profile"
        data-test="link-profile"
      >
        <UserPicture
          :user="user"
          width="32"
          height="32"
        />
        <span>{{ user.name }}</span>
      </router-link>
      <a
        href="#"
        class="header__logout"
        data-test="logout"
        @click.prevent="$logout"
        ><span>Выйти</span></a
      >
    </div>
  </header>
</template>

<script>
import { mapState, mapGetters } from "vuex";
import { logout } from "@/common/mixins";

export default {
  name: "AppLayoutHeader",
  mixins: [logout],
  computed: {
    ...mapState("Auth", ["user"]),
    ...mapGetters("Cart", ["totalSum"]),
  },
};
</script>

<style lang="scss" scoped>
.header {
  position: fixed;
  width: 100%;
  box-sizing: border-box;
}
</style>
