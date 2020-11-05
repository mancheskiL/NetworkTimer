<template>
    <div class="container">
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
            input:''
        }
    },
    methods: {
        submit() {
            axios({
                method: 'get',
                url: 'http://192.168.178.43:2000/timer',
                headers: {
                    'Content-Type': 'appliation/x-www-form-urlencoded',
                }
            })
                .then((response) => {
                    console.log(response)
                    ipcRenderer.send('new-window')
                    this.input = ''
                })
                .catch((error) => {
                    console.log(error)
                })
        },
    }
}
</script>

<style scoped>
    button{
        padding:10px;
        position:absolute;
        background-color:blueviolet;
        border-radius: 10px;
    }
    .submit{
        top:20%;
        right: 40%;
        width: 20%;
    }
</style>