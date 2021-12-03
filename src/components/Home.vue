<template>
  <Header />
  <h3>Hello {{ name }}, welcome on home page</h3>

  <table>
    <thead class="table">
      <tr>
        <th>name</th>
        <th>address</th>
        <th>Contact</th>
        <th>Action</th>
      </tr>
    </thead>
    <tbody>
      <!-- <tr v-for="(item,i) in restaurant" :key="i"> -->
      <tr v-for="item in restaurant" :key="item.id">
        <td>{{ item.name }}</td>
        <td>{{ item.address }}</td>
        <td>{{ item.contact }}</td>
        <td>
          <router-link :to="'/update/' + item.id">update</router-link> ||

          <button v-on:click="delResturant(item.id)">delete</button>
        </td>
      </tr>
    </tbody>
  </table>
</template>
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  name: "Home",
  data() {
    return {
      name: "",
      restaurant: [],
    };
  },
  methods: {
    async delResturant(id) {
      console.log(id);
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      if (result.status == 200) {
          this.loaddata();
      }
    },
    async loaddata() {
      let user = localStorage.getItem("user-info");
      this.name = JSON.parse(user).name;
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      console.warn(result);
      this.restaurant = result.data;
    },
  },
  async mounted() {
    this.loaddata();
  },
  components: {
    Header,
  },
  
};
</script>

 <style>
table {
  margin-left: 38%;
  margin-top: 105px;
}
td {
  width: 160px;
  height: 40px;
}
</style>