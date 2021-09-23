<template>
<img class ="logo" src="../assets/rslogo.jpg"/>
<h1>Sign Up</h1>

<form action="#" style=" padding: 50px; margin: 20px;">
  <div class="container">
    <input type="text" v-model="name" placeholder="Enter Name...">
    <input type="email" v-model="email" placeholder="Enter Email...">
    <input type="password" v-model="password" placeholder="Enter Password...">

    <div class="clearfix">
      <button v-on:click="signUp" type="submit" classs="signupbtn">Sign Up</button>
    </div>
  </div>
</form>
</template>

<script>
import axios from 'axios';
export default {
    name: 'Sign Up',

    data() {
      return {
        name: '', 
        email: '',
        password: ''
      }
    },
    methods: {
      async signUp()
      {
        let result = await axios.post("http://localhost:3000/users",{
          email: this.email,
          password: this.password,
          name: this.name,
        });

        console.warn(result);
        if(result.status==201)
        {
          
          localStorage.setItem("user-info",JSON.stringify(result.data))
          this.$router.push({name:"Home"})
        }
      }
    }
}
</script>

<style>
    .logo{
        width: 100%
    }

   * {box-sizing: border-box;}

   /* Full-width input fields */
   input[type=text], input[type=password], input[type=email] {
     width: 100%;
     padding: 15px;
     margin: 5px 0 22px 0;
     display: inline-block;
     border: 1px solid grey;
     border-radius: 5px;

   }

   input[type=text]:focus, input[type=password]:focus {
     background-color: #ddd;
     outline: none;
   }

   /* Set styles for buttons */
   button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background: skyblue;
    color: white;
    cursor: pointer;
    border-radius: 5px;
   }

   button:hover {
     opacity: 1;
   }

   /* adding padding to container elements */
   .container {
     padding: 16px;
   }

</style>
