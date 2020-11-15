<template>
    <div class="container">
        <p>{{ message }}</p>
        <input id='input' v-model="input" placeholder="Enter a time">
        <button v-on:click="submit" class="submit">Submit</button>
    </div>
</template>

<script>
const { ipcRenderer } = require('electron')
const axios = require('axios')


export default {
    name: 'Container',
    data() {
        return {
            input:'',
            message:''
        }
    },
    methods: {
        submit() {
            if (this.input.includes(':')){
                axios({
                    method: 'get',
                    url: 'http://192.168.178.43:3000/timer',
                    headers: {
                        'Content-Type': 'appliation/x-www-form-urlencoded',
                    },
                    params: {
                        time: this.input
                    }
                })
                    .then((response) => {
                        console.log(response)
                        ipcRenderer.send('new-window', [response['data'][0]])
                        this.input = ''
                        this.message = `URL to find your timer: ${response['data'][0]}`
                    })
                    .catch((error) => {
                        console.log(error)
                    })
            } else {
                this.message = 'Time must include a ":"'
            }
        },
    }
}
</script>

<style scoped>
    button{
        padding:10px;
        background-color:rgb(255, 4, 4);
        border-radius: 10px;
        display: block;
        margin: auto;
        margin-top: 10px;
        text-align: center;
        color: white;
        font-size: 20px;
        font-weight: bold;
    }
    .submit{
        top:20%;
        right: 40%;
    }
</style>