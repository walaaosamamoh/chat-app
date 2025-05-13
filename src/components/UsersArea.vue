<template>
    <div class="users-area">
        <div class="user-profile">
            <div class="avatar"><img class="profile-pic" :src= "currentUser.userpic" /></div>
            <div class="info">
                <p>{{currentUser.username}}</p>
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
                    <img class="profile-pic" :src= "user.userpic" />
                    </div>
                    <div class="user-info">
                    <p>{{ user.username }}</p>
                    <span v-if="messages">{{ user.lastMessage }}</span>
                    <span v-else>No message available </span>
                    </div>
                    <span class="checkActive" :class="{'active': user.isActive ===true}" > <i class="fas fa-circle"></i></span>
                </div>
            </div>            
            <div v-else> No user found related to your search</div>
        </div>
        </div>
    </div>
</template>

<script>
export default{
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
        }
    },

    methods:{
        showInput(){
            this.show = !this.show;
            this.search =''
        },
        handleLogout(){
            this.$router.push( {name:'login'})
        },
    }
}
</script>

<style>
.users-area{
    width: 30%;
    overflow:hidden;
}

.user-profile{
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    border-bottom: 1px solid #ccc;
}

.avatar{
    margin-right: 17px;
    width: 45px;
    height: 45px;
}

.profile-pic{
    border-radius: 50%;
    object-fit: cover;
    width: 100%;
    height: 100%;
}

.info, .user-info{
    flex: 1;
}

.info p, .user-info p{
    font-weight: 500;
    margin-bottom: 0;
    text-align: left
}

.info span{
    font-size:14px
}

.logout{
    background-color: rgba(0, 0, 0, 80%);
    color: #fff;
    font-size:16px;
    padding: 6px 12px;
    font-size:16px;
    padding: 6px 12px;
    border-radius: 6px;
    border: none;
    cursor:pointer
}

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
}

.users-list .search{
    display : flex;
    align-items:center;
    margin-bottom:15px;
    margin-bottom:15px;
}

.users-list .search span{
    flex: 1;
    margin-right:5px;
}

.users-list .search div{  
    padding:5px 13px;
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
    padding:0 10px;
    height: 35px;
    padding:0 10px;
    height: 35px;
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

.user-item .checkActive{
    margin-right:0
}

.user-item i{
    font-size:12px;
    font-size:12px;
    color:#ccc
}

.user-item .active i{
    color:green
}

.user-info span{
    color:rgba(0,0,0,70%);
    font-size:14px
}

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

</style>