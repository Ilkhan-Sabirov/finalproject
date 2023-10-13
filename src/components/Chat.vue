<template>
    <div v-if="username">
       <div class="chat">
        <h2 style="color: white;">Чат</h2>
        <div class="text" v-for = "message in messages" :key='message.id'>
            {{message.user}}: {{message.text}}
        </div>
        <div v-show="emptyMsg" class="empty">Текущих сообщений нет</div>
       </div>
       <input class="chati" placeholder="введите сообщение" v-model='newMessage'/>
       <button class="btni" @click="sendMessage">Отправить</button>
       <button class="btni" @click="delMessage">Удалить</button>
    </div>
    <div v-else>
        для авторизации перейдите по <router-link style="text-decoration: none;" to='/'>ссылке</router-link>
    </div>
</template>

<script>
export default {
    name: 'ChatComp',
    data(){
        return {
            messages: [],
            newMessage: '',
            emptyMsg: true,
            username: localStorage.getItem('username')
        }
    },

    computed() {
        localStorage.setItem('username', this.$route.query.username)
    },
    methods: {
        sendMessage(){
            if(!this.username){
                this.username = 'Аноним'
            }
            if(this.newMessage !== '') {
                this.emptyMsg = false
                console.log(this.newMessage);

                this.messages.push({id: new Date().getTime(), text: this.newMessage, user: this.username})
                this.saveChatRecords()
                this.newMessage = ''
            }else{
                alert('Введите сообщение')
            }
        },
        saveChatRecords(){
            const records = this.messages
            console.log(records);
            localStorage.setItem(`messages_${this.username}`, JSON.stringify(records))
        },
        delMessage() {
            this.messages = []
            localStorage.removeItem(`messages_${this.username}`, JSON.stringify(this.message))
            this.emptyMsg = true
        },
        loadChatRecords(){
            const records = JSON.parse(localStorage.getItem(`messages_${this.username}`))
            if(records){
                this.messages = records,
                this.emptyMsg = false
            }
        }
    },
    created(){
        this.loadChatRecords()
    }
}

</script>

<style>
   .chat {
    margin-top: 25px;
   }

   .chati {
    border-radius:10px; 
    padding:10px; 
    width:80%; 
    border:2px solid black; 
    box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
    margin-top: 10px;
   }

   .btni {
    display: inline-block;	
	box-sizing: border-box;
	padding: 0 15px;
	margin: 0 15px 15px 0;
	outline: none;
	border: none;  
	border-radius: 4px;
	height: 36px;
	line-height: 36px;
	font-size: 14px;
	font-weight: 500;
	text-decoration: none;
	color: #fff;
	background-color: #1a73e8;
	position: relative;
	overflow:hidden;
	vertical-align: top;
	cursor: pointer;
	user-select: none;
	appearance: none;
	touch-action: manipulation; 
	z-index: 1;
    border-radius: 25px;
    margin-top: 10px;
   }

   .text {
    color: aliceblue;
   }

   .empty {
    color: aliceblue;
   }
</style>