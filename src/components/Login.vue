   <template>
  <img src="../assets/download.png" class="logo" alt="" />
  <h1>Login</h1>
  <div class="login">
    <input type="text" v-model="email" placeholder="Enter Email" />
    <input type="password" v-model="password" placeholder="Enter password" />
    <button v-on:click="login">Login</button>
    <p>
      <router-link to="/sign-up">Sign Up</router-link>
    </p>
  </div>
</template>
   <script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    async login() {
      let result = await axios.get(
        `http://localhost:3000/users?email=${this.email}&password=${this.password}`
      );
      
      if (result.status == 200 && result.data.length > 0) {
        //  alert("sign up done");
        localStorage.setItem("user-info", JSON.stringify(result.data[0]));
        this.$router.push({ name: "Home" });
      }
    },
  },
   mounted(){
        //  console.log('mount');
        let user = localStorage.getItem("user-info")
        if(user){
            this.$router.push({name:"Home"})
        }
     }
};
</script>

   <style>
.logo {
  width: 350px;
}
.login input {
  width: 300px;
  height: 40px;
  padding-left: 20px;
  display: block;
  margin-right: auto;
  margin-left: auto;
  margin-bottom: 20px;
  border: 1px solid skyblue;
}
.login button {
  width: 320px;
  height: 40px;
  border: 1px solid skyblue;
  color: #fff;
  background-color: skyblue;
  cursor: pointer;
}
</style>