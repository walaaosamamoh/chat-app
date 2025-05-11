<template>
  <div class="signup-page page">
      <div class="container">
          <h2>El-Bayt Chat App</h2>
  
          <div class="errorMsg" v-if="message">{{ message }}</div>
          
          <form @submit.prevent="handleSubmit" novalidate>
              <div class="full-name">
                <div>
                  <label >First Name</label>
                  <input type="text" placeholder="First name" v-model="fname" required>
                </div>
                <div>
                  <label >Last Name</label>
                  <input type="text" placeholder="Last name" v-model="lname" required>
                </div>
              </div>

              <label >Email Address</label>
              <input type="email" placeholder="Enter your email" v-model="email" required>
  
              <label >Password</label>
              <div class="input-wrapper">          
                  <input :type="showPassword ? 'text':'password'" placeholder="Enter your password" v-model="password" required>
                  <span class="toggle-password" :class="{'show':showPassword}" @click ="togglePassword"><i :class="showPassword?'fas fa-eye-slash':'fas fa-eye'"></i></span>
              </div>

              <label >Select Image</label>
              <input type="file" placeholder="Choose File" @change="handleFileUpload">
               
              <button type="submit">Continue to Chat</button>
  
          </form>
          <p>Already signed up? <router-link :to="{name:'login'}">Login now</router-link> </p>
  
          <img class="logo" src="../assets/etoo play.png" alt="logo"/>
  
      </div>
  </div>
  </template>
  
  <script>
  export default{
      props:['question','page'],
      data(){
          return{
             showPassword:false,
             email:'',
             password: '',
             message:'',
             fname:'',
             lname:'',
             file:'',
          }
      },
      methods:{
          togglePassword(){
              this.showPassword= !this.showPassword
          },
          isValidEmail(email){
            const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            return re.test(email)
          },
          handleFileUpload(e){
            this.file= e.target.files[0];
          },
          handleSubmit(){
              if (!this.fname || !this.lname || !this.email || !this.password){
                  const emptyField = document.querySelectorAll('input:invalid');
                  if(emptyField.length>0){
                    emptyField[0].focus();
                    emptyField[0].reportValidity()
                  }
                  this.message = "All input fields are required!";
                  return
              }
               if (!this.isValidEmail(this.email)) {
                  this.message = this.email +' is not a valid email!'
              } else if(!this.file){
                  this.message ='Please upload an image file - jpeg, png, jpg'
              } else{
                  const reader = new FileReader();
                  reader.onload = ()=>{
                    const savedUsers = JSON.parse(localStorage.getItem('users')) || [];
                    savedUsers.push({
                    id: Date.now(),
                    username : this.fname + ' ' + this.lname,
                    useremail: this.email,
                    userpassword: this.password,
                    userpic : reader.result,
                    isActive: true
                  })
                  localStorage.setItem('users', JSON.stringify(savedUsers));
                  localStorage.setItem('currentUser', JSON.stringify(savedUsers[savedUsers.length - 1]));
                  
                  this.$router.push('./home')
                  }
                  reader.readAsDataURL(this.file)
              }     
          }
      }
  }
  </script>
  
  <style>
  .container form .full-name{
    display: flex;
    gap:15px;
    width:80%
  }

  .container form .full-name div{
    display: flex;
    flex-direction: column;
    flex:1;
    min-width:0;
  }

  .container form input[type="file"]{
    border:none;
    font-size: 16px;
    padding: 0;
  }  

  @media(max-width:767px){
    .container form .full-name{
      flex-direction:column;
      gap:0;
      width:100%
    }
  }
</style>
