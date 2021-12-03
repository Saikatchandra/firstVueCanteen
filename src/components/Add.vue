<template>
  <Header />
  <h3>Add restaurant</h3>
  <form>
    <input
      type="text"
      name="name"
      v-model="restaurant.name"
      placeholder="Enter name"
    />
    <input
      type="text"
      name="address"
      v-model="restaurant.address"
      placeholder="Enter address"
    />
    <input
      type="text"
      name="contact"
      v-model="restaurant.contact"
      placeholder="Enter contact"
    />
    <button type="button" v-on:click="addRestaurant">Submit</button>
  </form>
</template>
<script>
import axios from "axios";
import Header from "./Header.vue";
export default {
  name: "Add",
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  components: {
    Header,
  },
  methods: {
    async addRestaurant() {
      console.log(this.restaurant);
      let result = await axios.post("http://localhost:3000/restaurant", {
        name: this.restaurant.name,
        address: this.restaurant.address,
        contact: this.restaurant.contact,
      });
      console.log(result);
      if(result.status == 201){
          this.$router.push({name:'Home'});
      }
    },
  },
  mounted() {
    //  console.log('mount');
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
  },
};
</script>

 <style>
form input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-right: auto;
  margin-left: auto;
  margin-bottom: 20px;
  border: 1px solid skyblue;
}
form button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
  cursor: pointer;
}
</style>