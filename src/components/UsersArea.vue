<template>
    <div class="users-area">
        <div class="user-profile">
<<<<<<< HEAD
            <div class="avatar"><img class="profile-pic" :src= "currentUser.userpic" /></div>
            <div class="info">
                <p>{{currentUser.username}}</p>
=======
            <div class="avatar"><img class="profile-pic" src= "../assets/verne-ho-0LAJfSNa-xQ-unsplash.jpg" /></div>
            <div class="info">
                <p>Walaa Osama</p>
>>>>>>> a56cd2b (first commit)
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
<<<<<<< HEAD
=======

>>>>>>> a56cd2b (first commit)
        </div>
        <div class='users'>
            <div v-if="filterdUsers.length">
                <div v-for="user in filterdUsers" :key="user.id"
                class="user-item" :class="{ active: selectedUser && selectedUser.id === user.id }"
                @click="$emit('select-user', user)" >
                    <div class="avatar">
<<<<<<< HEAD
                    <img class="profile-pic" :src= "user.userpic" />
                    </div>
                    <div class="user-info">
                    <p>{{ user.username }}</p>
                    <span v-if="messages">{{ user.lastMessage }}</span>
                    <span v-else>No message available </span>
                    </div>
                    <span :class="{'active': user.isActive ===true}" > <i class="fas fa-circle"></i></span>
                </div>
            </div>            
            <div v-else> No user found related to your search</div>
=======
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
>>>>>>> a56cd2b (first commit)
        </div>
        </div>
    </div>
</template>

<script>
export default{
<<<<<<< HEAD
    props: ['users','currentUser'],

    data() {
        return {
        selectedUser: null,
        show: true,
        search:''
       }
    },

    computed:{
          filterdUsers(){
            if(!Array.isArray(this.users))return [];
            return this.users.filter(user=>
                user.id != this.currentUser.id &&
                user.username.toLowerCase().startsWith(this.search.toLowerCase())
            )
=======
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
>>>>>>> a56cd2b (first commit)
        }
    },

    methods:{
        showInput(){
            this.show = !this.show;
            this.search =''
        },
        handleLogout(){
<<<<<<< HEAD
            this.$router.push( {name:'login'})
=======
            this.$router.push({name:'login'})
>>>>>>> a56cd2b (first commit)
        },
    }
}
</script>

<style>
.users-area{
    width: 30%;
<<<<<<< HEAD
=======
    padding:10px;
>>>>>>> a56cd2b (first commit)
    overflow:hidden;
}

.user-profile{
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    border-bottom: 1px solid #ccc;
}

.avatar{
<<<<<<< HEAD
    margin-right: 17px;
    width: 45px;
    height: 45px;
}

.profile-pic{
    border-radius: 50%;
=======
    width: 50px;
    height: 50px;
    border-radius: 50%;
    overflow: hidden;
    margin-right: 17px;
}

.user-profile .profile-pic{
>>>>>>> a56cd2b (first commit)
    object-fit: cover;
    width: 100%;
    height: 100%;
}

.info, .user-info{
    flex: 1;
}

.info p, .user-info p{
<<<<<<< HEAD
    font-weight: 500;
    margin-bottom: 0;
    text-align: left
}

.info span{
    font-size:14px
=======
    font-size:18px;
    font-weight:500;
    margin-bottom:0;
    text-align:left
>>>>>>> a56cd2b (first commit)
}

.logout{
    background-color: rgba(0, 0, 0, 80%);
    color: #fff;
<<<<<<< HEAD
    font-size:16px;
    padding: 6px 12px;
=======
    padding: 8px 14px;
    font-size: 17px;
>>>>>>> a56cd2b (first commit)
    border-radius: 6px;
    border: none;
    cursor:pointer
}

<<<<<<< HEAD
@media(max-width:767px){
    .users-area{
        width: 40%;
        padding:0
    }

    .user-profile{
        justify-content:space-between;
        padding-bottom: 10px;
    }

    .profile-pic{
        width:2.1875rem;
        height:2.1875rem
    }

    .user-profile .info{
        display:none
    }

    .logout{
        padding: 5px 8px;
        font-size: 0.875rem;
    }

    .info p,.user-info p{
        font-size:1rem
    }

    .info span,.user-info span{
        font-size:0.875rem
    }
}

.users-list{
    margin:20px 0;
=======
.users-list{
    margin:25px 0;
>>>>>>> a56cd2b (first commit)
}

.users-list .search{
    display : flex;
    align-items:center;
<<<<<<< HEAD
    margin-bottom:15px;
}

.users-list .search span{
=======
    margin-bottom:25px
}

.users-list .search span{
    font-size:18px;
>>>>>>> a56cd2b (first commit)
    flex: 1;
    margin-right:5px;
}

.users-list .search div{  
<<<<<<< HEAD
    padding:5px 13px;
=======
    padding:8px 15px;
>>>>>>> a56cd2b (first commit)
    border-radius:0 6px 6px 0;
    cursor:pointer
}

.users-list .search div.hide{
<<<<<<< HEAD
    background-color: rgba(0, 0, 0, 80%);
    color:#fff
=======
   background-color: rgba(0, 0, 0, 80%);
   color:#fff
>>>>>>> a56cd2b (first commit)
}

.users-list .search input{
    width:100%;
    border: 1px solid #d0c8c8;
    border-radius: 6px 0 0 6px;
<<<<<<< HEAD
    padding:0 10px;
    height: 35px;
=======
    padding: 10px;
>>>>>>> a56cd2b (first commit)
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
<<<<<<< HEAD
    font-size:12px;
=======
    font-size:14px;
>>>>>>> a56cd2b (first commit)
    color:#ccc
}

.user-item .active i{
    color:green
}

.user-info span{
    color:rgba(0,0,0,70%)
}
<<<<<<< HEAD

@media(max-width:767px){
    .users-list{
        margin:15px 0
    }
    .users-list .search span,.user-info span{
        font-size:12px;
    }
    .users-list .search div{
        padding:3px 5px
    }
    .users-list .search input{
        padding: 5px 10px
    }
    .user-item .avatar{
        width:30px;
        height:30px
    }
    .user-item i{
        font-size:10px
    }
    .user-info p{
        font-size:14px
    }
}
=======
>>>>>>> a56cd2b (first commit)
</style>