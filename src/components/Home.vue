<template>
<Header />
    <h3>Hello, welcome on home page</h3>
</template>
<script>
import Header from "./Header.vue"
export default {
    name: "Home",
    components:{
        Header
    },
     mounted(){
        //  console.log('mount');
        let user = localStorage.getItem("user-info")
        if(!user){
            this.$router.push({name:"SignUp"})
        }
     }

}
</script>

 <style>
 
 </style>