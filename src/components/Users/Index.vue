<template>
  <div>
    <h1>Get All Users</h1>
    <div>จํานวนผู้ใช้งาน {{ users.length }}</div>
    <div v-for="user in users" v-bind:key="user.id">
      <div>title: {{ user.title }}</div>
      <div>author: {{ user.author }} </div>
      <div>total_page: {{ user.email }}</div>
      <div>publisher: {{ user.password }}</div>
      <div>category: {{ user.password }}</div>
      <div>price: {{ user.password }}</div>
      <p>
        <button v-on:click="navigateTo('/user/' + user.id)">
          ดูข้อมูลผู้ใช้
        </button>
        <button v-on:click="navigateTo('/user/edit/' + user.id)">
          แกไขข้อมูล
        </button>
        <button v-on:click="deleteUser(user)">ลบข้อมูล</button>
      </p>
      <hr />
    </div>
  </div>
</template>
<script>
import UserServices from "@/services/UserService";
export default {
  data() {
    return {
      users: []
    };
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user) {
      let result = confirm("Want to delete?");
      if (result) {
        try {
          await UserServices.delete(user);
          this.refreshData()
        } catch (err) {
          console.log(err);
        }
      }
    },
    async refreshData() {
      this.users = (await UserServices.index()).data;
    }
  },
  async created() {
    this.users = (await UserServices.index()).data;
  }
};
</script>
<style scoped></style>
