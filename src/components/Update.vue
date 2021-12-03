<template>
  <Header />
  <h3>update restaurant</h3>
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
    <button type="button" v-on:click="updateRestaurant">Submit</button>
  </form>
</template>
<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  name: "Update",
  data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
  methods: {
   async updateRestaurant() {
      console.log("up", this.restaurant);
      let result = await axios.put("http://localhost:3000/restaurant/" + this.$route.params.id, {
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
  components: {
    Header,
  },
  async mounted() {
    //  console.log('mount');
    let user = localStorage.getItem("user-info");
    if (!user) {
      this.$router.push({ name: "SignUp" });
    }
    const result = await axios.get(
      "http://localhost:3000/restaurant/" + this.$route.params.id
    );
    // console.log(result);
    this.restaurant = result.data;
  },
};
</script>

 <style>
</style>