<template>
  <div>
    <label for="upload" class="button">upload</label>
    <input type="file" style="visibility:hidden" id="upload" accept=".json,.csv" @change="onFileUpload">
    <label for="upload-sql" class="button">upload vers s3</label>
    <input type="file" style="visibility:hidden" id="upload-sql" accept=".sql" @change="onFileUpload">
  </div>
</template>

<script>
export default {
  name: 'App',
  methods: {
    onFileUpload: function(event) {
      let file = event.target.files[0];
      console.log('test');
      let formData = new FormData();
      formData.append('file', file);
      this.uploadFile(formData);
    },
    uploadFile: function(file) {
      fetch('url', {
        method: 'POST',
        body: file,
      })
      .then(res => res.json())
      .then(success => console.log(success))
      .catch(error => console.error('Error @uploadFile : ' + error));
    }
  }

}
</script>

<style>
  .button {
    font-size: 1rem;
    font-family: sans-serif;
    color: #fff;
    background: #219ebc;
    padding: .5rem 2rem;
    border-radius: .5rem;
    cursor: pointer;
    transition: all 200ms ease-in-out;
  }
  .button:hover {
    background: #15768f;
  }
</style>
