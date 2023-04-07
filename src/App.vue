<template>
  <div id="container" ref="graphDom">111</div>
</template>

<script setup lang="ts">
import { Graph } from '@antv/x6'
import { onMounted, ref } from 'vue'

// vue3响应式的画布DOM
const graphDom = ref<HTMLElement | null>(null)

// 需要等组件完全挂载好后，DOM准备完毕，才能读取DOM
onMounted(() => {
  const data = {
    // 节点
    nodes: [
      {
        id: 'node1', // String，可选，节点的唯一标识
        shape: 'rect', // 使用 rect 渲染
        x: 40,       // Number，必选，节点位置的 x 值
        y: 40,       // Number，必选，节点位置的 y 值
        width: 80,   // Number，可选，节点大小的 width 值
        height: 40,  // Number，可选，节点大小的 height 值
        label: 'hello', // String，节点标签
      },
      {
        id: 'node2', // String，节点的唯一标识
        shape: 'ellipse', // 使用 ellipse 渲染
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

  // 初始化画布
  const graph = new Graph({
    // 挂载DOM节点
    container: graphDom.value as HTMLElement,
    // 宽高
    width: 800,
    height: 600,
    // 背景
    background: {
      color: '#fffbe6', // 设置画布背景颜色
    },
    // 网格
    grid: {
      size: 10,      // 网格大小 10px
      visible: true, // 渲染网格背景
    },
    // grid: true,
  })

  // 从给定的JSON数据里渲染画布
  graph.fromJSON(data)

  // 画布缩放
  // 0 不变 -.5 缩小一半 -.75 缩小到原来的3/4 .5 放大到原来的1.5倍
  // 其实这里传参的是对原始缩放比例进行加减，再乘现在的尺寸
  // 公式为
  // newSize = (1 + zoomFactor) * oldSize
  graph.zoom(.2)

  // 画布平移
  // x 正右负左 y 正下负上
  graph.translate(100, 50)

})
</script>

<style scoped>
</style>
