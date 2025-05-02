<template>
    <div class="users-area">
        <div class="user-profile">
            <div class="avatar"><img class="profile-pic" src= "../assets/verne-ho-0LAJfSNa-xQ-unsplash.jpg" /></div>
            <div class="info">
                <p>Walaa Osama</p>
                <span>Active now</span>
            </div>
            <button class="logout" @click="handleLogout">Logout</button>
        </div>
        <div class="users-list">
        <div class="search">
            <span>
                <span v-if="show">Select a user to start chat</span>
                <input v-else type="text" v-model="search" placeholder="Enter name to search"/>
            </span>
            <div :class="{'hide' : !show}">
            <i :class="show?'fas fa-search':'fas fa-times'" @click="showInput" ></i>
            </div>

        </div>
        <div class='users'>
            <div v-if="filterdUsers.length">
                <div v-for="user in filterdUsers" :key="user.id"
                class="user-item" :class="{ active: selectedUser && selectedUser.id === user.id }"
                @click="$emit('select-user', user)" >
                    <div class="avatar">
                    <img class="profile-pic" :src= "user.img" />
                    </div>
                    <div class="user-info">
                    <p>{{ user.name }}</p>
                    <span v-if="user.lastMessage">{{ user.lastMessage }}</span>
                    <span v-else>No message available </span>
                    </div>
                    <span :class="{'active': user.isActive ==='true'}"><i class="fas fa-circle"></i></span>
                </div>
            </div>
            <div v-else>No user found related to your search</div>
        </div>
        </div>
    </div>
</template>

<script>
export default{
    props: ['users'],

  data() {
    return {
      selectedUser: null,
      show: true,
      search:''
    }},

    computed:{
      filterdUsers(){
        return this.users.filter(user=>
            user.name.toLowerCase().startsWith(this.search.toLowerCase())
        )
        }
    },

    methods:{
        showInput(){
            this.show = !this.show;
            this.search =''
        },
        handleLogout(){
            this.$router.push({name:'login'})
        },
    }
}
</script>

<style>
.users-area{
    width: 30%;
    padding:10px;
    overflow:hidden;
}

.user-profile{
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    border-bottom: 1px solid #ccc;
}

.avatar{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 17px;
}

.user-profile .profile-pic{
    object-fit: cover;
    width: 100%;
    height: 100%;
}

.info, .user-info{
    flex: 1;
}

.info p, .user-info p{
    font-size:18px;
    font-weight:500;
    margin-bottom:0;
    text-align:left
}

.logout{
    background-color: rgba(0, 0, 0, 80%);
    color: #fff;
    padding: 8px 14px;
    font-size: 17px;
    border-radius: 6px;
    border: none;
    cursor:pointer
}

.users-list{
    margin:25px 0;
}

.users-list .search{
    display : flex;
    align-items:center;
    margin-bottom:25px
}

.users-list .search span{
    font-size:18px;
    flex: 1;
    margin-right:5px;
}

.users-list .search div{  
    padding:8px 15px;
    border-radius:0 6px 6px 0;
    cursor:pointer
}

.users-list .search div.hide{
   background-color: rgba(0, 0, 0, 80%);
   color:#fff
}

.users-list .search input{
    width:100%;
    border: 1px solid #d0c8c8;
    border-radius: 6px 0 0 6px;
    padding: 10px;
}

.users-list .search input:focus{
    outline:none
}

.users-list .users .user-item{
    display: flex;
    border-bottom: 1px solid #eee;
    padding: 15px 15px 15px 0;
    align-items: center;
}

.user-item .avatar{
    width:40px;
    height:40px;
}

.user-item i{
    font-size:14px;
    color:#ccc
}

.user-item .active i{
    color:green
}

.user-info span{
    color:rgba(0,0,0,70%)
}
</style>