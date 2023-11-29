<script setup>
    // import ref
    import { ref, reactive, onMounted } from 'vue';

    // {{ }} gebruik je om iets af te printen
    let message = ref(""); // kan reflecteren naar de front-end gebruik int, string, boolean
    let allMessages = reactive({
        data: ["Heel", "Even", "Simple","Doen"],
    }); 

    // function onMounted
    onMounted(async() => {
        try {
            const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
            const data = await response.json();
            allMessages.data = data;
        } catch (error) {
            console.error("error:", error); 
        }
    });

    // function sendMessage
    const SendMessage = () => {
        allMessages.data.push(message.value);
        message.value = ""; //.value moet je gebruiken als je met ref werkt, heeft niks te maken met het tekstvak
    };
    

</script>

<template>
  <div>
    <ul>
        <li v-for="m in allMessages.data">{{ m }}</li> 
    </ul>

    <div>
        <input v-model="message" type="text" placeholder="" />
        <button @click="SendMessage">Send</button>
    </div>

  </div>
</template>

<style scoped> 

</style>