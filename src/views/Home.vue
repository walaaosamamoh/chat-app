<template >
    <div class="home-page">
        <div class="container">
<<<<<<< HEAD
            <UsersArea :users="users" :currentUser="currentUser" @select-user= "handleSelection" :messages="messages" />
            <ChatArea :users="users" :selected-user="selectedUser" :messages="messages"/>
=======
            <UsersArea :users="users" @select-user= "handleSelection"/>
            <ChatArea :selected-user="selectedUser"/>
>>>>>>> a56cd2b (first commit)
        </div>
    </div>
</template>

<script>
import UsersArea from '../components/UsersArea'
import ChatArea from '../components/ChatArea'

export default{
    components:{UsersArea, ChatArea},

    data() {
    return {
<<<<<<< HEAD
      // users: [
      //   {id:1, name:'Ahmed Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true',lastMessage:'hi'},
      //   {id:2, name:'W L',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false'},
      //   {id:3, name:'Omer Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false',lastMessage:'hello'},
      //   {id:4, name:'Mona Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true'},
      // ],
      users:'',
      currentUser:'',
      selectedUser: '',
      messages:{}
    }
},

mounted(){
  this.users= JSON.parse(localStorage.getItem('users'));
  this.currentUser= JSON.parse(localStorage.getItem('currentUser'));
  this.users.forEach(user=>{
            if(!this.messages[user.id]){
                this.messages[user.id]=[];
            }
        });
        console.log(this.messages)

},

=======
      users: [
        {id:1, name:'Ahmed Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true',lastMessage:'hi'},
        {id:2, name:'W L',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false'},
        {id:3, name:'Omer Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false',lastMessage:'hello'},
        {id:4, name:'Mona Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true'},
      ],
      selectedUser: ''
    }
},

>>>>>>> a56cd2b (first commit)
// computed: {
//     filteredMessages() {
//       if (!this.selectedUser) return [];
//       return this.messages.filter(msg => 
//         (msg.sender === this.currentUser.id && msg.receiver === this.selectedUser.id) ||
//         (msg.sender === this.selectedUser.id && msg.receiver === this.currentUser.id)
//       );
//     }
//   },
   
  methods: {
    handleSelection(user){
        this.selectedUser = user;
    },
  }
}
</script>

<style>
.home-page{
    display: flex;
<<<<<<< HEAD
    padding:45px 10px;
     height:100vh
  }
=======
    height: 100vh;
}
>>>>>>> a56cd2b (first commit)

.home-page .container{
    gap :20px;
    flex-direction:row;
    width:100%;
<<<<<<< HEAD
    margin: 0 auto;
   
}

@media(max-width:767px){
  .home-page{
    padding:25px 10px;
  }
  .home-page .container{
    margin: 0 auto;
    gap:5px
  }
=======
    margin: 45px 10px
>>>>>>> a56cd2b (first commit)
}
</style>