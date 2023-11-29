<!-- <script setup>
    import { ref, reactive, onMounted } from 'vue'; 

    let videoUrl = ref(""); // met : ga je binden als dit verandert gaat de video ook veranderen
    let videos = reflective({ 
        data: [],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
        .then((response) => response.json())
        .then((data) => {
            console.log(data);
            videos.data = data.record.videos;
            videoUrl.value = videos.data[0].video; // hier moet je de counter + 1 doen om de nieuwe video te krijgen
        });
    });

</script>

<template>
  <div>
    <video :src="videoUrl" controls autoplay muted loop></video>
  </div>
</template>

<style scoped> 

</style> -->

<script setup>
    import { ref, reactive, onMounted } from 'vue';

    //define emits
    const emit = defineEmits(['update:videoDescription']);
    
    let videoUrl = ref("");
    let videos =reactive({
        data:[],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15") // deze link aanpassen met je eigen
        .then((res) => res.json())
        .then((data) => {
            videos.data = data.record.videos;
            videoUrl.value = videos.data[0].videoUrl;

            //emit
            emit('update:videoDescription', videos.data[0].description);
        });
    });
</script>

<template>
  <div>
    <video :src="videoUrl" controls autoplay muted loop></video>
  </div>
</template>

<style scoped>

</style>