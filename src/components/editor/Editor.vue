<template>
  <div class="upload-action">
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
</template>

<script>
export default {
  props: ["files", "previewSize", "loadImage"]
};
</script>