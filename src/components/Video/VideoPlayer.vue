<script setup>
    import { ref, reactive, onMounted } from 'vue';

    //define emits
    const emits = defineEmits(["update:videoDescription"]); // deze link aanpassen met je eigen
    
    let videoUrl = ref(""); // met : ga je binden als dit verandert gaat de video ook veranderen
    let videos =reactive({
        data:[],
    });

    onMounted(() => {
        fetch("https://api.jsonbin.io/v3/b/6548ef9954105e766fcc2c15")
        .then((res) => res.json())
        .then((data) => {
            videos.data = data.record.videos;
            videoUrl.value = videos.data[0].video;

            // emit event
            emits("update:videoDescription",videos.data[0].description);
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