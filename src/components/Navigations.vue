<template>
    <div class="containernav">
        <nav>
            <router-link class="navr" to='/'>Домашняя страница</router-link>
            <router-link class="navr" to='/chat'>Чат</router-link>
            <router-link class="navr" to='/nba'>Узнать команды NBA</router-link>
        </nav>
    </div>
</template>

<script>
export default {
    name: 'NavComp'
}

</script>

<style>
      .containernav {
        display: flex;
        justify-content: center;
        width: 100%;
    }

    nav {
        width: 500px;
        height: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 30px;  
    }

    .navr {
        color: white;
        text-decoration: none;
        
    }

</style>
