<template>
  <section id="upload">
    <h2>Hochladen</h2>
    <form @submit.prevent="uploadFile">
      <input type="file" @change="onFileSelect" />
      <button type="submit">Hochladen</button>
    </form>
    <div id="fileList" v-if="uploadedFiles.length > 0">
      <h3>Hochgeladene Dateien:</h3>
      <ul>
        <li v-for="file in uploadedFiles" :key="file.fileUrl">
          <a :href="file.fileUrl" target="_blank">{{ file.fileName }}</a>
        </li>
      </ul>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      selectedFile: null,
      uploadedFiles: [],
    };
  },
  methods: {
    onFileSelect(event) {
      this.selectedFile = event.target.files[0];
    },
    async uploadFile() {
      if (!this.selectedFile) {
        alert("Bitte wähle eine Datei aus!");
        return;
      }

      const formData = new FormData();
      formData.append("file", this.selectedFile);

      const apiURL = process.env.VUE_APP_BACKEND_API_URL;

      try {
        const response = await fetch(`${apiURL}/upload`, {
          method: "POST",
          body: formData,
        });
        const data = await response.json();
        if (response.ok) {
          this.uploadedFiles.push({ fileUrl: data.fileUrl, fileName: data.fileName });
        } else {
          alert(`Fehler: ${data.message}`);
        }
      } catch (error) {
        console.error("Fehler beim Hochladen:", error);
        alert("Fehler beim Hochladen der Datei.");
      }
    },
  },
};
</script>

<style scoped>
#upload {
  margin: auto;
  max-width: 600px;
  text-align: center;
}

#fileList ul {
  margin-top: 1rem;
  list-style: none;
  padding: 0;
}

#fileList li a {
  color: #007bff;
  text-decoration: none;
}
</style>
