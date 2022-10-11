<template>
<div class="container is-max-desktop">
  <form class="has-text-left" @submit.prevent="upload">
    <div class="field">
      <label class="label">foodId</label>
      <div class="control">
        <input class="input" type="number" v-model="query.foodId" required>
      </div>
    </div>
    <div class="field">
      <label class="label">type</label>
      <div class="control">
        <div class="select">
          <select v-model="query.type" required>
            <option value="image">image</option>
            <option value="autre">autre</option>
          </select>
        </div>
      </div>
    </div>
    <div class="file">
      <label class="file-label">
        <input class="file-input" type="file" name="resume" @change="onFileChange" required>
        <span class="file-cta">
          <span class="file-label">
            {{ file ? file.name : 'Choose a file…' }}
          </span>
        </span>
      </label>
    </div>
    <br>

    <div class="field is-grouped">
      <div class="control">
        <button class="button is-link" type="submit">Submit</button>
      </div>
    </div>
  </form>
</div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'HelloWorld',
  data() {
    return {
      query: {
        foodId: '19',
        type: 'image',
      },
      file: null,
    }
  },
  methods: {
    onFileChange(e) {
      var files = e.target.files || e.dataTransfer.files;
      if (!files.length)
        return;
      this.file = files[0];
    },
    async upload() {
      try {
        const formData = new FormData();
        formData.append('image', this.file);
        const response = await axios.post(`http://localhost:1337/files?foodId=${this.query.foodId}&type=${this.query.type}`, formData);
        console.log(response);
      } catch (error) {
        console.error(error);
      }
    }
  },
}
</script>
