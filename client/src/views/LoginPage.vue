<script>
import { mapActions, mapWritableState } from "pinia";
import { useLoginMethodStore } from "../stores/loginMethod";
export default {
  data() {
    return {
      loginField: {
        email: "",
        password: "",
      },
    };
  },
  computed: {},
  methods: {
    ...mapActions(useLoginMethodStore, [
      "login",
      "handleCredentialResponse",
      "googleSignInMethod",
    ]),
    async loginMethod() {
      let email = this.loginField.email;
      let password = this.loginField.password;
      await this.login(email, password); // panggil store login
    },
  },
  mounted() {
    this.googleSignInMethod();
  },
};
</script>

<template>
  <!-- Login Section -->
  <section id="login-section" class="gradient-custom">
    <div class="container py-5">
      <div class="row d-flex justify-content-center align-items-center">
        <div class="col-12 col-md-8 col-lg-6 col-xl-5">
          <div class="card bg-dark text-white" style="border-radius: 1rem">
            <div class="card-body p-5 text-center">
              <form id="form-Login" @submit.prevent="loginMethod">
                <div class="mb-md-5 mt-md-4 pb-5">
                  <h2 class="fw-bold mb-2">Login</h2>
                  <p class="text-white-50 mb-5">Please fill the field below!</p>
                  <div class="form-outline form-white mb-4">
                    <label class="form-label" for="input-Login-email"
                      >Email :</label
                    >
                    <input
                      v-model="loginField.email"
                      type="email"
                      id="input-Login-email"
                      class="form-control form-control-lg"
                      placeholder="enter your email..."
                    />
                  </div>
                  <div class="form-outline form-white mb-4">
                    <label class="form-label" for="input-Login-password"
                      >Password :</label
                    >
                    <input
                      v-model="loginField.password"
                      type="password"
                      id="input-Login-password"
                      class="form-control form-control-lg"
                      placeholder="enter your password..."
                    />
                  </div>
                  <button
                    class="btn btn-outline-light btn-lg px-5"
                    type="submit"
                  >
                    Login
                  </button>
                </div>
              </form>
              <div>
                <p class="mb-0">
                  Dont have account?
                  <a
                    @click.prevent="this.$router.push('/register')"
                    class="text-white-50 fw-bold"
                    >Sign In</a
                  >
                </p>
              </div>
              <div class="mt-2" id="google-login"></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#login-section {
  background: linear-gradient(to right, rgb(17, 203, 144), rgb(37, 252, 187));
}
</style>
