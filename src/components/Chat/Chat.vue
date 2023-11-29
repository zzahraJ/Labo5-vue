<script setup>
    //import ref
    import { ref, reactive, onMounted } from 'vue';

    let message = ref(""); // kan reflecteren naar de front-end gebruik int, string, boolean
    let allMessages= reactive({
        data: ["Heel", "Even", "Simple","Doen"],
    }); 

    const name = "ZAHRA";

    // function onMounted
    onMounted(async () => {
        const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/");
        const data = await response.json();
        allMessages.data = data;
    }); 

    //function SendMessage
    const SendMessage = async () => {
        const newMessage ={
            user: name,
            text: message.value,
        }
    const response = await fetch("https://lab5-p379.onrender.com/api/v1/messages/", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
        },
        body: JSON.stringify(newMessage),
    });

    allMessages.data.push(newMessage);// new message toevoegen aan de array
    message.value = ""; //.value moet je gebruiken als je met ref werkt, maakt het tekstvak terug leeg
};

</script>

<template>
    <div>
        <ul>
            <li v-for="m in allMessages.data" :key="m.id">{{ m.user}}: {{ m.text }}</li> 
        </ul>
        <div>
            <input v-model="message" type="text" placeholder="">
            <button @click="SendMessage">Send</button>
        </div>
    </div>
</template>

<style scoped>

ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}
li {
    padding: 8px;
    margin-bottom: 8px;
    background-color: #f2f2f2;
    border-radius: 4px;
}

</style>

