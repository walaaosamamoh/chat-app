<template >
    <div class="home-page">
        <div class="container">
            <UsersArea :users="users" @select-user= "handleSelection"/>
            <ChatArea :selected-user="selectedUser"/>
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
      users: [
        {id:1, name:'Ahmed Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true',lastMessage:'hi'},
        {id:2, name:'W L',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false'},
        {id:3, name:'Omer Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'false',lastMessage:'hello'},
        {id:4, name:'Mona Mohamed',img:'/images/verne-ho-0LAJfSNa-xQ-unsplash.jpg',isActive:'true'},
      ],
      selectedUser: ''
    }
},

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
    height: 100vh;
}

.home-page .container{
    gap :20px;
    flex-direction:row;
    width:100%;
    margin: 45px 10px
}
</style>