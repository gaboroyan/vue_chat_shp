<template>
    <div id="app">
        <Container>
            <ChatWindow>
              <ChatMessenger v-bind:username='message.author'
              v-bind:datetime='message.datetime'
              v-for='(message, i) in messages' 
              v-bind:key='i'>{{ message.text }}</ChatMessenger>
            </ChatWindow>
        </Container>
    </div>
</template>

<script>
import Container from './components/Container.vue'
import ChatMessenger from './components/ChatMessenger.vue'
import ChatWindow from './components/ChatWindow.vue'

export default {
    name: 'App',
        components: {
            Container,
            ChatMessenger,
            ChatWindow
        },
        data() {
            return {
                messages: []
            }
        },
        methods: {
            getMessages() {
                  this.axios.get('http://37.77.104.246/api/chat/getmessages.php')
                  .then( (resp)=>{
                      this.messages = resp.data
                  } )
            }
        },
        mounted() {
            this.getMessages();
        }
    }
</script>

<style>
body {
  margin: 0;
  background-color: #f9f9fa;
}
</style>

