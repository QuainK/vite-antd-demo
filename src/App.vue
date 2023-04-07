<template>
  <div id="container" ref="graphDom">111</div>
</template>

<script setup lang="ts">
import { Graph } from '@antv/x6'
import { onMounted, ref } from 'vue'

const graphDom = ref<HTMLElement | null>(null)

// 需要等组件完全挂载好后，DOM准备完毕，才能读取DOM
onMounted(() => {
  const data = {
    // 节点
    nodes: [
      {
        id: 'node1', // String，可选，节点的唯一标识
        x: 40,       // Number，必选，节点位置的 x 值
        y: 40,       // Number，必选，节点位置的 y 值
        width: 80,   // Number，可选，节点大小的 width 值
        height: 40,  // Number，可选，节点大小的 height 值
        label: 'hello', // String，节点标签
      },
      {
        id: 'node2', // String，节点的唯一标识
        x: 160,      // Number，必选，节点位置的 x 值
        y: 180,      // Number，必选，节点位置的 y 值
        width: 80,   // Number，可选，节点大小的 width 值
        height: 40,  // Number，可选，节点大小的 height 值
        label: 'world', // String，节点标签
      },
    ],
    // 边
    edges: [
      {
        source: 'node1', // String，必须，起始节点 id
        target: 'node2', // String，必须，目标节点 id
      },
    ],
  }

  const graph = new Graph({
    container: graphDom.value as HTMLElement,
    width: 800,
    height: 600
  })

  graph.fromJSON(data)
})
</script>

<style scoped>
#container {
  background: #eee;
}
</style>
