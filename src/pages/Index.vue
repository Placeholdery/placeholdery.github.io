<template>
  <Layout>
    <div v-show="Object.keys(files).length" class="action-bar">
      <ul style="display: flex; align-items: center; justify-content: space-between;">
        <li>Select</li>
        <li>Colors</li>
        <li>Height*Width</li>
        <li>
          <Edit3Icon />
        </li>
        <li>
          <TypeIcon />
        </li>
        <li>
          <Trash2Icon />
        </li>
      </ul>
    </div>
    <div v-if="!Object.keys(files).length && !Object.keys(previewSize).length" class="uploader">
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
      <ul class="list" style="list-style: none; margin: 0;">
        <li v-for="file in files" :key="file.name">
          <div style="display: flex; align-items: center; justify-content: space-between;">
            <div>
              <img @load="loadImage" style="width: 250px;" :src="file.image" alt="file.name" />
            </div>
            <div>
              <p>
                <ImageIcon />
                {{ file.name }}
              </p>
              <p>
                <FileTextIcon />
                {{ file.type }}
              </p>
            </div>
            <div>
              <p>
                <Edit3Icon />
                {{ previewSize.width/10 + 'px' }}
              </p>
              <p>
                <TypeIcon />Arial
              </p>
            </div>
            <p>Colors</p>
            <div
              class="image-placeholder"
              :style="{ width: previewSize.width + 'px', height: previewSize.height + 'px', fontSize: previewSize.width/10 + 'px' }"
            >{{ file.dimensions.width }} x {{ file.dimensions.height }}</div>
            <div>
              <TrashIcon />
            </div>
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
import {
  ImageIcon,
  Trash2Icon,
  TrashIcon,
  FileTextIcon,
  Edit3Icon,
  TypeIcon
} from "vue-feather-icons";

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
    upload: function() {
      const fileInput = this.$refs["fileinput"];
      fileInput.click();
    },
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
    ImageIcon,
    Trash2Icon,
    TrashIcon,
    FileTextIcon,
    Edit3Icon,
    TypeIcon
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
