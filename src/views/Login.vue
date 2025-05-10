<template>
<div class="login-page page">
    <div class="container">
        <h2>El-Bayt Chat App</h2>

        <div class="errorMsg" v-if="message"> {{ message }}</div>
        
        <form @submit.prevent="handleSubmit" novalidate>
            <label >Email Address</label>
            <input type="email" placeholder="Enter your email" v-model="email" required>

            <label >Password</label>
            <div class="input-wrapper">          
                <input :type="showPassword ?'text':'password'" placeholder="Enter your password" v-model="password" required>
                <span class="toggle-password" :class="{'show':showPassword}" @click ="togglePassword"><i :class="showPassword?'fas fa-eye-slash':'fas fa-eye'"></i></span>
            </div>
             
            <button type="submit">Continue to Chat</button>

        </form>
        <p> Not yet signed up? <router-link :to="{name:'signup'}">Signup now</router-link> </p>

        <img class="logo" src="../assets/etoo play.png" alt="logo"/>

    </div>
</div>
</template>

<script>
export default{
    props: ['question','page'],
    data(){
        return{
           showPassword:false,
           email:'',
           password: '',
           message:''
        }
    },
    methods:{
        togglePassword(){
            this.showPassword= !this.showPassword
        },
        handleSubmit(){
            if (!this.email || !this.password){
                const emptyField =document.querySelectorAll('input:invalid');
                if(emptyField.length>0){
                    emptyField[0].focus();
                    emptyField[0].reportValidity()
                }
                this.message = "All input fields are required!";
                return
            }
            
                const savedUsers = JSON.parse(localStorage.getItem('users')) || [];
                console.log(savedUsers)

                const foundUser = savedUsers.find(user => 
                user.useremail === this.email);

                if(!foundUser){
                    this.message= this.email +' - This email not Exist!';
                    return;
                }

                if(foundUser.userpassword !== this.password){
                    this.message ='Email or Password is Incorrect!';
                    return;
                }

                localStorage.setItem('currentUser', JSON.stringify(foundUser));
                this.$router.push({name:'home'});
            }     
        }
    }
</script>
