<template>
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
</template>

<style scoped>
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
  props: ["files"],
  components: {
    Edit3Icon,
    TypeIcon,
    Trash2Icon
  }
};
</script>