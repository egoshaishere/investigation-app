<template>
  <div>
    <ToolBar />
    <WorkSpace />
  </div>
</template>

<script>
import ToolBar from './ToolBar.vue'
import WorkSpace from './WorkSpace.vue'



export default {
    name: "Investigation",
    components: {
      ToolBar,
      WorkSpace
    }

}
</script>

<style>

</style>