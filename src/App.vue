<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import { ref } from 'vue'
import Paragraph from './components/Paragraph.vue';
let list = ref([{ title: '古巴比伦王颁布了汉谟拉比法典' },
  { title: '刻在黑色的玄武岩距今已经三千七百多年' },
  { title: '你在橱窗前凝视碑文的字眼' },
  { title: '我却在旁静静欣赏你那张我深爱的脸' },
  { title: '祭司神殿征战弓箭是谁的从前' },
  { title: '喜欢在人潮中你只属于我的那画面' },
  { title: '经过苏美女神身边我以女神之名许愿' },
  { title: '思念像底格里斯河般的蔓延' },
  { title: '当古文明只剩下难解的语言' },
  { title: '传说就成了永垂不朽的诗篇' },
  { title: '我给你的爱写在西元前' },
  { title: '深埋在美索不达米亚平原' },
  { title: '几十个世纪后出土发现' },
  { title: '泥板上的字迹依然清晰可见' },
  { title: '我给你的爱写在西元前' },
  { title: '深埋在美索不达米亚平原' },
  { title: '用楔形文字刻下了永远' },
  { title: '那已风化千年的誓言' },
  { title: '一切又重演' }
  ]
)
</script>

<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <div class="app">
    <div class="flex">
      
    </div>
    <div class="lyrics-board">
      <Paragraph :list="list"></Paragraph>
    </div>
  </div>
</template>

<style lang="scss">
html, body {
  height: 100%;
}
body, div, p {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  // height: 100%;
  padding: 50px 0;
  height: 100%;
  overflow-y: scroll;
  background-position: center top;
  background-size: cover;
  background: radial-gradient(ellipse at top left, rgba(105,155,200,1) 0%,rgba(181,197,216,1) 57%);
  position: relative;
}
.lyrics-board {
  margin: 50px auto;
  width: 400px;
  position: relative;
  overflow: hidden;
  border-radius: 10px;
  z-index: 1;
  // background: radial-gradient(ellipse at top left, rgba(105,155,200,1) 0%,rgba(181,197,216,1) 57%);
  &:after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    // background-color: rgba(255,255,255,0.8);
    // background-color: rgba(255,255,255,0.3);
    z-index: -1;
    background: rgba(255, 255, 255, .3);
    // background-position: center top;
    // background-size: cover;
    // background-attachment: fixed;
    // background: radial-gradient(ellipse at top left, rgba(105,155,200,1) 0%,rgba(181,197,216,1) 57%);
    filter: blur(20px);
  }
}
</style>
