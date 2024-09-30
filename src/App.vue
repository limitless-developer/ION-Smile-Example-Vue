<script setup>
import HelloWorld from './components/HelloWorld.vue'


const HOST = import.meta.env.VITE_SMILE_HOST;
const TOKEN = import.meta.env.VITE_SMILE_TOKEN;

import 'ion-smile/style.css';
import ionSmile from 'ion-smile';

const config = {
                credential:{
                    host    : HOST, 
                    token   : TOKEN, 
                    userkey : "user1", 
                    session : "example-session"
                },
                dom:{
                    moveable:true // default false
                }
            }

const smile = new ionSmile(config);
    
    smile.init();

    smile.on("ready",(e)=>{
        if(e.module="ai" && e.status){
            smile.start()
        }
    });
    smile.on("alert",(e)=>{
        console.log(e);
        
        if(e.status){ // status = true, if fraud detected
            // alert(e.description)
        }
    });
</script>

<template>
  <div>
    <a href="https://vitejs.dev" target="_blank">
      <img src="/vite.svg" class="logo" alt="Vite logo" />
    </a>
    <a href="https://vuejs.org/" target="_blank">
      <img src="./assets/vue.svg" class="logo vue" alt="Vue logo" />
    </a>
  </div>
  <HelloWorld msg="Vite + Vue" />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
