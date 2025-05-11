<template>
    <div class="chat-area">
        <div class="chat-header">
            <div class="avatar"><img class="profile-pic" :src="selectedUser.userpic" /></div>
            <div class="info">
                <p v-if="selectedUser"> {{ selectedUser.username}} </p>
                <span v-if="selectedUser && selectedUser.isActive===true">Active now</span>
                <span v-else-if="selectedUser && selectedUser.isActive===false">Offline now</span>
            </div>
        </div>
        <div class="chat-box">
            <div class="reciever">
                <div class="avatar" v-if="selectedUser.lastMessage">
                    <img class="profile-pic" :src="selectedUser.userpic" />
                </div>
                <div class=" lastmsg" v-if="selectedUser.lastMessage">{{ selectedUser.lastMessage }}</div>
            </div>
            <div class="sender">
                <div class="sender-message" v-for="message in messages[selectedUser.id]" :key="message.msg" >
                    <div>{{ message.msg }}</div>
                </div>
            </div>
            <p v-if="!selectedUser || messages[selectedUser.id].length===0 "> No messages are available. Once you send message .they will appear here.</p>
        </div>
        <div class="send-msg">
            <input type="text" placeholder="Type a message here..." v-model="msg"/>
            <span @click="sendMessage"><i class="fas fa-paper-plane"></i></span>
        </div>
    </div>
</template>

<script>
export default{
    props: ['users', 'selectedUser','messages'],
    data(){
        return{
            msg:''
        }
    },

    methods:{
       sendMessage(){
        if(this.selectedUser){
            if(this.msg.trim()!==''){
            this.messages[this.selectedUser.id].push({msg: this.msg.trim() });
           }
           this.msg='';
        }
       }
    }
}
</script>

<style>
.chat-area{
    flex:1;
    /* min-width:70%; */
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

.sender-message{
    display:flex;
    flex-direction:column;
}
.sender-message div{
    padding:8px 10px;
    border-radius: 20px 20px 0 20px;
    background-color: rgba(0, 0, 0, 80%);
    color: #fff;
    width:fit-content;
    margin-bottom:10px;
    align-self: flex-end;
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
    width:100%;
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

@media(max-width:767px){
    .chat-box p{
        font-size:14px
    }
    .send-msg{
        padding:2px
    }
}
</style>