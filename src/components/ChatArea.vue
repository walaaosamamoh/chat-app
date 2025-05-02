<template>
    <div class="chat-area">
        <div class="chat-header">
            <div class="avatar"><img class="profile-pic" :src="selectedUser.img" /></div>
            <div class="info">
                <p v-if="selectedUser">{{ selectedUser.name }} </p>
                <span v-if="selectedUser && selectedUser.isActive==='true'">Active now</span>
                <span v-else-if="selectedUser && selectedUser.isActive==='false'">Offline now</span>
            </div>
        </div>
        <div class="chat-box">
            <div class="reciever">
                <div class="avatar" v-if="selectedUser.lastMessage"><img class="profile-pic" :src="selectedUser.img" /></div>
                <span class=" lastmsg" v-if="selectedUser.lastMessage">{{ selectedUser.lastMessage }}</span>
            </div>
            <p v-if="!selectedUser.lastMessage">No messages are available. Once you send message they will appear here.</p>
        </div>
        <div class="send-msg">
            <input type="text" placeholder="Type a message here..." v-model="msg"/>
            <span @click="sendMessage"><i class="fas fa-paper-plane"></i></span>
        </div>
    </div>
</template>

<script>
export default{
    props: ['selectedUser'],

}
</script>

<style>
.chat-area{
    width:70%;
    display:flex;
    flex-direction:column;
}

.chat-header{
    display: flex;
    align-items: center;
    padding:0 40px 20px;
}

.chat-box{
    flex:1;
    background-color:#eee;
    padding:20px;
    margin-right:0;
    position: relative
}

.chat-box p{
    text-align:center;
    position:absolute;
    left:50%;
    top:50%;
    transform: translate(-50%,-50%);
    
}
.reciever{
    display: flex;
    align-items:center
}
.chat-box .avatar{
    width:40px;
    height:40px;
    display:inline-block
}
.lastmsg{
    padding:15px;
    border-radius: 20px 20px 20px 0;
    background-color:#fff
}
.newmsg{
    padding:15px;
    border-radius: 20px 20px 0 20px;
    background-color:rgba(0,0,0,80%);
    color:#fff;
    margin-right:0
}
.send-msg{
    padding:20px 30px 0;
    display:flex;
}

.send-msg input{
    flex:1;
    border: 1px solid #d0c8c8;
    border-radius: 6px 0 0 6px;
    padding: 10px;
    margin-right:5px
}

.send-msg input:focus{
    outline:none
}

.send-msg span{
    background-color:rgba(0,0,0,60%);
    color:#fff;
    padding:10px 15px;
    border-radius: 0 6px 6px 0;
    display:flex;
    justify-content:center;
    align-items:center
}
</style>