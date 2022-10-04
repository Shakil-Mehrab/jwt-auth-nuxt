<template>
  <div>
    <form @submit.prevent="userLogin">
      <div>
        <label>Email</label>
        <input type="text" v-model="form.email" />
      </div>
      <div>
        <label>Password</label>
        <input type="text" v-model="form.password" />
      </div>
      <div>
        <button type="submit">Submit</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  middleware: ["redirectIfAuthenticated"],
  data() {
    return {
      form: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith("local", {
          data: this.form,
        });

        this.$router.replace({
          name: "index",
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
