<template>
  <div>
    <app-action-bar :files="files"></app-action-bar>
    <app-uploader :files="files" :previewSize="previewSize" :fileUpload="fileUpload"></app-uploader>
    <app-editor :files="files" :previewSize="previewSize" :loadImage="loadImage"></app-editor>
  </div>
</template>

<style>
.fileinput {
  display: none;
}
</style>

<script>
import Uploader from "./uploader/Uploader.vue";
import ActionBar from "./editor/ActionBar.vue";
import Editor from "./editor/Editor.vue";

export default {
  metaInfo: {
    title: "Homepage"
  },
  data: () => {
    return {
      files: {},
      previewSize: {}
    };
  },
  methods: {
    loadImage: function(e) {
      const {
        target: { offsetHeight, offsetWidth }
      } = e;
      this.previewSize = {
        height: offsetHeight,
        width: offsetWidth
      };
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
    AppActionBar: ActionBar,
    AppUploader: Uploader,
    AppEditor: Editor
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

.upload-action {
  padding: 0 25px;
  height: 100%;
  overflow-y: scroll;
}

.action-bar {
  position: absolute;
  background: #fff;
  width: calc(100% - 50px);
  top: 0;
  left: 0;
  padding: 15px 25px;
  box-shadow: 0 -15px 20px 10px #000;
}

.action-bar ul {
  list-style: none;
}

.image-placeholder {
  background-color: aliceblue;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
  color: rgba(38, 50, 56, 0.5);
}

.list li {
  margin-bottom: 15px;
}

.list li:last-child {
  margin-bottom: 0;
}
</style>
