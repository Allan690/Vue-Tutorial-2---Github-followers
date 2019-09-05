<template>
<el-container class="cardContainer">
    <div>
        <input v-model="userName" placeholder="Enter the username of the github user...">
        <button v-on:click="fetchGithubFollowers">Submit</button>
    </div>
    <el-container style="display: inline-flex; flex-wrap: wrap">
        <div class="card" v-for="follower in followersArray" v-bind:key="follower.id">
            <img :src="follower.avatar_url" alt="Avatar" style="width:100%">
            <div class="container">
                <h4><b>{{ follower.login}}</b></h4>
                <p>{{follower.html_url }}</p>
            </div>
        </div>
    </el-container>
</el-container>
</template>

<script>
    import axios from 'axios';

    export default {
        name: 'GithubUserFollowers',
        data() {
            return { userName: '', followersArray: [] }
        },
        methods: {
            async fetchGithubFollowers() {
                const results = await axios({
                    method: 'get',
                    url: `https://api.github.com/users/${this.userName}/followers`,
                    Authorization: `token ${process.env.GITHUB_TOKEN}`
                });
                const { data } = results;
                this.followersArray = data;
            }
        }
    }
</script>

<style scoped>
.cardContainer {
    display: flex;
    flex-flow: wrap;
    justify-content: space-between;
}
    input {
        margin-right: 20px;
        margin-left: 300px;
        width: 250px;
        border-style: none;
        outline: none;
    }
    button {
        padding: 10px 15px 10px 10px;
        border-radius: 25px;
        outline: none;
    }
.card {
    box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);
    transition: 0.3s;
    width: 40%;
    border-radius: 5px;
    margin: 50px;
}

.card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0,0,0.2);
}

img {
    border-radius: 5px 5px 0 0;
}

.container {
    padding: 2px 16px;
}
</style>
