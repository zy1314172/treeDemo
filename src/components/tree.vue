<template>
  <div>
    <li @dblclick="addProject(treeData)">
      {{ treeData.name }}
      <span v-show="Folder" @click="Open = !Open"
        >[{{ !Open ? "+" : "-" }}]</span
      >
      <ul v-show="Open">
        <tree
          v-for="(item, index) in treeData.children"
          :key="index"
          :treeData="item"
          @add-item="addItem($event)"
          @add-project="$emit('add-project', $event)"
        ></tree>
        <li v-show="treeData.children" @click="addItem(treeData)">+</li>
      </ul>
    </li>
  </div>
</template>

<script>
export default {
  name: "tree",
  props: {
    treeData: {
      type: Object,
      default: {},
    },
  },
  data() {
    return {
      Open: false,
    };
  },
  computed: {
    Folder() {
      return this.treeData.children;
    },
  },
  methods: {
    addItem(item) {
      this.$emit("add-item", item);
    },
    addProject(item) {
      if (!this.Folder) {
        this.$emit('add-project', item)
        this.Open = true
      }
    },
  },
};
</script>

<style>
</style>