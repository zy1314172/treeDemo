<template>
  <div>
    <ul>
      <tree :treeData="treeData" @add-item="addItem" @add-project="addProject"></tree>
    </ul>
  </div>
</template>

<script>
import tree from '@/components/tree.vue'

export default {
  name: 'App',
  data(){
    return {
      treeData:{
        name: "一级",
        children: [
          { name: "二级" },
          { name: "二级" },
          {
            name: "二级",
            children: [
              {
                name: "三级",
                children: [{ name: "四级" }, { name: "四级" }]
              },
              { name: "三级" },
              { name: "三级" },
              {
                name: "三级",
                children: [{ name: "四级" }, { name: "四级" }]
              }
            ]
          }
        ]
      }
    }
  },
  components:{
    tree
  },
  methods:{
    addItem(item) {
      item.children.push({
        name: 'new stuff',
      })
    },
    addProject(item) {
      this.$set(item,'children',[])
      this.addItem(item)
    },
  }
}
</script>

<style>

</style>
