<template>
    <div class="home">
        <div v-if="isAuthentificated">
            <div style="font-size: 25px; color: beige;">Приветсвуем вас, уважаемый <b>{{username}}</b></div>
            <button class="btn" @click="logout">Выйти</button>
        </div>
        <div v-else>
            <label style="font-size: 20px; color: white;">Введите имя:</label>
            <input class="homei" v-model='username'/>
            <button class="btn" @click="login">Сохранить</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'HomePage',
    data(){
        return {
            isAuthentificated: false,
            username: ''
        }
    },

    created(){
        if(localStorage.getItem('isAuthentificated')){
            this.isAuthentificated = true,
            this.username = localStorage.getItem('username')
        }
    },
    methods: {
        login(){
            if(this.username !== ''){
                console.log(this.username);

                this.isAuthentificated = true
                localStorage.setItem('isAuthentificated', true);
                localStorage.setItem('username', this.username)

                this.$router.push({
                    name: 'Chat',
                    query: {username: this.username}
                })
            }else {
                console.log('Введите данные');
            }
        },
        logout(){
                this.isAuthentificated = false,
                this.username = '',
                localStorage.removeItem('isAuthentificated'),
                localStorage.removeItem('username')
            }
    }
}

</script>

<style>
   .homei {
    border-radius:10px; 
    padding:10px; 
    width:80%; 
    border:2px solid black; 
    box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
    margin-top: 10px;
   }
   .btn {
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

   .home {
    padding-top: 120px;
   }
</style>