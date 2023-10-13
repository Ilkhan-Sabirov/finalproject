<template>
    <div>
        <div style="margin-bottom: 10px; color: white"><b>Команды NBA:</b></div>
        <div v-if='isLoad'>Загрузка данных...</div>
        <div v-else>
            <div v-for="(el) in teamData" :key="el.id">
                <div style="color: rgb(204, 199, 199);">{{el.id}}. <b>Abbreviation:</b>{{el.abbreviation}}  <b style="margin-left: 20px;">Division:</b>" {{el.division}} <img src="https://avatars.mds.yandex.net/i?id=e51c0bb71789882fb6fc9e3608f8c47904342b10-7593510-images-thumbs&n=13&exp=1"
                style="width: 15px; height: 15px"
                @click="removeTeam(el.id)"
                /></div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'TestApi',
    data(){
        return {
            teamData: [],
            isLoad: true
        }
    },
    mounted(){
        const url = 'https://free-nba.p.rapidapi.com/teams?page=0';
const options = {
	method: 'GET',
	headers: {
		'X-RapidAPI-Key': 'aa898a2cd6msh867c8f7088aab5ep13dce7jsn76dbee8cf0ab',
		'X-RapidAPI-Host': 'free-nba.p.rapidapi.com'
	}
};


    fetch(url, options)
    .then((res) => res.json())
    .then((res) => {
        console.log(res);
        this.teamData = res.data
        this.isLoad = false
    })
    },
    methods: {
        removeTeam(id) {
            this.teamData = this.teamData.filter((el) => el.id !== id)
        }
    }
}

</script>

<style>
   
</style>