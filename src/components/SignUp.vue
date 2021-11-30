<template>
<img src="../assets/download.png" class="logo" alt="">
    <h3>Sign Up</h3>
    <div class="register">
        <input type="text" v-model="name" placeholder="name">
        <input type="email" v-model="email" placeholder="email">
        <input type="password" v-model="password" placeholder="password">
        <button v-on:click="signUp" >Sign up</button>
    </div>
</template>

 <script>
 import axios from 'axios'
 export default{
     name: "SignUp",
     data(){
         return{
             name: '',
             email: '',
             password: ''
         }
     },
     methods:{
        async signUp(){
             console.log('sdfsd',this.name,this.email,this.password);
             let result = await axios.post("http://localhost:3000/users",{
                 name: this.name,
                 email: this.email,
                 password: this.password
             });
             console.log(result);
             if(result.status == 201){
                //  alert("sign up done");
                localStorage.setItem("user-info",JSON.stringify(result.data))
                this.$router.push({name:"Home"})
             }
         }
     },
     mounted(){
        //  console.log('mount');
        let user = localStorage.getItem("user-info")
        if(user){
            this.$router.push({name:"Home"})
        }
     }
 }
 </script>

  <style>
  .logo{
      width: 350px
  }
  .register input{
       width: 300px;
       height: 40px;
       padding-left: 20px;
       display: block;
       margin-right:auto;
       margin-left: auto;
       margin-bottom: 20px;
       border: 1px solid skyblue;
  }
  .register button{
      width: 320px;
      height: 40px;
      border: 1px solid skyblue;
      color: #fff;
      background-color: skyblue;
      cursor: pointer;
  }
  </style>