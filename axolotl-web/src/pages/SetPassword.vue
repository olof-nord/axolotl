<template>
  <div class="set-password">
    <h5 v-translate>Info</h5>
    <p v-translate>
      Setting a password is not adviced on devices short in memory. Restart is
      required!
    </p>
    <div
      v-if="passwordError"
      class="alert alert-danger"
      role="alert"
      v-translate
    >
      Passwords don't match
    </div>
    <div
      v-if="passwordUnsafe"
      class="alert alert-danger"
      role="alert"
      v-translate
    >
      Unsafe password
    </div>
    <div
      v-if="currentPasswordWrong"
      class="alert alert-danger"
      role="alert"
      v-translate
    >
      Current password is wrong
    </div>
    <label for="passwordRepeat" class="text-primary" v-translate
      >New password</label
    >
    <password
      v-model="password"
      type="password"
      name="password"
      id="setPassword"
      :secureLength="7"
    />
    <div class="form-group">
      <label for="passwordRepeat" class="text-primary" v-translate
        >Repeat password</label
      >
      <input
        required
        v-model="passwordRepeat"
        type="password"
        name="passwordRepeat"
        id="passwordRepeat"
        class="form-control"
      />
    </div>
    <div class="form-group">
      <label for="passwordCurrent" class="text-primary" v-translate
        >Current password</label
      >
      <input
        required
        v-model="passwordCurrent"
        type="password"
        name="passwordCurrent"
        id="passwordCurrent"
        class="form-control"
      />
    </div>
    <button class="btn btn-primary" @click="setPassword()" v-translate>
      Set password
    </button>
  </div>
</template>

<script>
import Password from "vue-password-strength-meter";
export default {
  name: "setPasword",
  components: {
    Password,
  },
  methods: {
    setPassword() {
      const { password, passwordRepeat } = this;
      if (password.localeCompare(passwordRepeat) != 0) {
        this.passwordError = true;
      } else if (password.length < 7 && password.length > 0) {
        this.passwordUnsafe = true;
      } else {
        this.$store.dispatch("setPassword", {
          pw: this.password,
          cPw: this.passwordCurrent,
        });
      }
    },
  },
  data() {
    return {
      password: "",
      passwordCurrent: "",
      currentRepeat: "",
      passwordRepeat: null,
      passwordError: false,
      passwordUnsafe: false,
      currentPasswordWrong: false,
    };
  },
};
</script>
<style scoped>
.set-password {
  display: flex;
  flex-direction: column;
  padding-top: 30px;
}
.phoneInput {
  margin-top: 30px;
}
.btn {
  max-width: 300px;
  margin: auto;
  margin-top: auto;
  margin-top: 50px;
}
</style>
<style>
.Password {
  width: 100% !important;
  max-width: 100% !important;
  margin: 0 auto;
}
.Password__group #setPassword {
  display: block;
  width: 100%;
  height: calc(1.5em + 0.75rem + 2px);
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #495057;
  background-color: #fff;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.25rem;
}
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
