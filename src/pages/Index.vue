<template>
  <Layout>
    <div v-if="!Object.keys(files).length" class="uploader">
      <div>
        <image-icon size="10x" />
      </div>
      <div>
        <h2>Drag & Drop Image/s</h2>
        <p>or</p>
        <input @change="fileUpload" class="fileinput" type="file" multiple ref="fileinput" />
        <button @click="upload">Upload</button>
      </div>
    </div>
    <div v-else class="upload-action">
      <ul>
        <li v-for="file in files" :key="file.name">
          <div>
            <div>
              <img style="height: 100px;" :src="file.image" alt="file.name" />
            </div>
            <p>{{file.name}}</p>
            <ul v-if="file.dimensions">
              <li>Width: {{ file.dimensions.width }}</li>
              <li>Height: {{ file.dimensions.height }}</li>
            </ul>
          </div>
        </li>
      </ul>
    </div>
  </Layout>
</template>

<style>
.fileinput {
  display: none;
}
</style>

<script>
import { ImageIcon } from "vue-feather-icons";

export default {
  metaInfo: {
    title: "Homepage"
  },
  data: () => {
    return {
      files: {}
    };
  },
  methods: {
    upload: function() {
      const fileInput = this.$refs["fileinput"];
      fileInput.click();
    },
    fileUpload: function(e) {
      const {
        target: { files }
      } = e;
      if (files.length) {
        let actualFiles = {};
        for (let i = 0; i < files.length; i++) {
          const image = URL.createObjectURL(files[i]);
          actualFiles = {
            ...actualFiles,
            [i]: {
              name: files[i].name,
              image,
              type: files[i].type
            }
          };
        }
        this.setDimentions(actualFiles);
      }
    },
    setDimentions: function(files) {
      const imageKeys = Object.keys(files);
      const imageKeysLength = imageKeys.length;
      let count = 0;
      imageKeys.map(imageKey => {
        const file = files[imageKey];
        const imageReader = new window.Image();
        imageReader.src = file.image;
        imageReader.onload = () => {
          const width = imageReader.width;
          const height = imageReader.height;
          files[imageKey].dimensions = {
            width,
            height
          };
          count++;
          if (count === imageKeysLength) {
            this.files = files;
          }
        };
      });
    }
  },
  components: {
    ImageIcon
  }
};
</script>

<style>
.uploader {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
}
</style>
