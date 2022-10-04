<template>
  <div>
    welcome
    <form @submit.prevent="logout">
      <button type="submit">Logout</button>
    </form>

    {{ $auth.user.data.name }}
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  middleware: ["authIndent"],

  methods: {
    async logout() {
      try {
        await this.$auth.logout("local");
        this.$router.replace({
          name: "auth-login",
        });
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
