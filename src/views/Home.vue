<template>
  <div class="home">
    <h1>Sube cualquier video</h1>
    <input type="text" v-model="path">
    <S3FileUpload :obj="video" :dirName="path" />
  </div>
</template>

<script>
import S3FileUpload from "@/components/S3FileUpload";

export default {
  name: "Home",
  data() {
    return {
      path: "",
      video: null,
    };
  },
  components: {
    S3FileUpload,
  },
};
</script>


<style scoped>
.home {
}

.container-video {
  width: 800px;
  height: 500px;
}

.iframe-scren {
  width: 100%;
  height: 100vh;
}
</style>
