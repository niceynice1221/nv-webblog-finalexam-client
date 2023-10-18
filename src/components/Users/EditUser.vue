<template>
  <div>
    <h1>Edit Users</h1>
    <h1>Edit User</h1>
    <form v-on:submit.prevent="editUser">
      <p>title: <input type="text" v-model="user.title" /></p>
      <p>author: <input type="text" v-model="user.author" /></p>
      <p>total_page: <input type="text" v-model="user.total_page" /></p>
      <p>publisher: <input type="text" v-model="user.publisher" /></p>
      <p>category: <input type="text" v-model="user.category" /></p>
      <p>price: <input type="text" v-model="user.price" /></p>
    </form>
    <hr />
    <div>
      <p>: title{{ user.title }}</p>
      <p>author: {{ user.author }}</p>
      <p>total_page: {{ user.total_page }}</p>
      <p>publisher: {{ user.publisher }}</p>
      <p>category: {{ user.category }}</p>
      <p>price: {{ user.price }}</p>
      <p></p>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UserService";
export default {
  data() {
    return {
      user: {
        name: "",
        lastname: "",
        email: "",
        password: "",
        status: "active"
      }
    };
  },
  methods: {
    async editUser() {
      try {
        await UsersService.put(this.user);
        this.$router.push({
          name: "users"
        });
      } catch (err) {
        console.log(err);
      }
    }
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UsersService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  }
};
</script>
<style scoped></style>
