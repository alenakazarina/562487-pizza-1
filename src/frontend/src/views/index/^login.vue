<template>
  <PopupOverlay
    @click.self="closeLogin"
    @keydown.esc="closeLogin"
  >
    <div class="sign-form">
      <router-link
        to="/"
        class="close close--white"
        data-test="login-close"
      >
        <span class="visually-hidden">Закрыть форму авторизации</span>
      </router-link>
      <div
        class="sign-form__title"
        data-test="login-title"
      >
        <h1 class="title title--small">Авторизуйтесь на сайте</h1>
      </div>
      <LoginForm @close="closeLogin" />
    </div>
  </PopupOverlay>
</template>

<script>
import LoginForm from "@/modules/login/components/LoginForm";
import { isLoggedIn } from "@/middlewares";

export default {
  name: "Login",
  middlewares: [isLoggedIn],
  components: { LoginForm },

  methods: {
    closeLogin() {
      this.$router.push("/");
    },
  },
};
</script>
