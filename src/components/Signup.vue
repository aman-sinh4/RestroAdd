<template>
    <img src="../assets/logo.png" alt="" class="logo"/>
    <h1>SignUp</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" /> 
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">Sign Up</button>
        <p><router-link to="/login">Login</router-link></p>

    </div>
</template>

<script>
import axios from 'axios'
export default {
    name:'Signup',
    data(){
        return{
            name:'',
            email:'',
            password:''
        }
    },
    methods:{
        async signUp(){
            console.log(this.name, this.email, this.password)
            let result = await axios.post("http://localhost:3000/users",{
                email:this.email,
                name:this.name,
                password:this.password
            });
            console.log("result>>>",result);
            if(result.status==201){
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({name:'Home'})
            }
            
        }


    },
            mounted(){
            let user = localStorage.getItem('user-info');
            if(user){
                console.log("mounted")
                this.$router.push({name:'Home'})
            }
        }
}
</script>
