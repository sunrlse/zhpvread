<script setup>
import { onMounted, getCurrentInstance } from '@vue/runtime-core'
import Velocity from 'velocity-animate'
import { reactive } from 'vue'
import piaonOgg from '../assets/media/korg-m3r-grand-piano-c5.ogg'

let audioIns = null

const props = defineProps({
  list: {
    type: Array,
    default: [],
  },
})
const reactiveData = reactive({
  initedAnimation: false,
})
onMounted(() => {
  initAnimation()
  initPiano()
})
var iStartTop = 0
var iMinTop = -18
var iMaxTop = 18
var mouseEnterIndex = 0

function initAnimation() {
  const vm = getCurrentInstance()
  props.list.forEach((item, index) => {
    const $el = vm.refs['ref_list' + index]
    const spans = $el.children[0].children
    const spanArr = Array.prototype.slice.call(spans)
    spanArr.forEach((span) => {
      const left = span.offsetLeft
      span.style.left = left + 'px'
      span.addEventListener('mouseenter', wordMouseEnterSpring)
    })
  })
  reactiveData.initedAnimation = true
}

function wordMouseEnterSpring(e) {
  var target = e.target
  var $parent = target.parentNode
  $parent.onmouseout = null
  $parent.onmousemove = null
  var iStartY = e.clientY
  var index = target.getAttribute('data-i')
  mouseEnterIndex = index
  playPiano()
  $parent.onmousemove = function (pe) {
    var spans = $parent.children
    var spanArr = Array.prototype.slice.call(spans)
    spanArr.forEach((el) => {
      Velocity.animate(el, 'stop')
      el.removeEventListener('mouseenter', wordMouseEnterSpring)
      el.addEventListener('mouseenter', wordMouseEnterCurrentIndex)
    })
    var iMouseY = pe.clientY
    var iTop = iStartTop + (iMouseY - iStartY)

    if (iTop < iMinTop || iTop > iMaxTop) {
      console.log('parent if iStartTop ', iStartTop)
      spanArr.forEach((el) => {
        Velocity.animate(el, { top: iStartTop }, 500, 'spring')
        el.addEventListener('mouseenter', wordMouseEnterSpring)
        el.removeEventListener('mouseenter', wordMouseEnterCurrentIndex)
      })
      $parent.onmouseleave = null
      $parent.onmousemove = null
    } else {
      for (var i = 0; i < spanArr.length; i++) {
        if (iMouseY > iStartY) {
          var iSpanTop = iTop - Math.abs(i - mouseEnterIndex)
          if (iSpanTop < iStartTop) {
            iSpanTop = iStartTop
          }
        } else if (iMouseY < iStartY) {
          var iSpanTop = iTop + Math.abs(i - mouseEnterIndex)
          if (iSpanTop > iStartTop) {
            iSpanTop = iStartTop
          }
        }
        spanArr[i].style.top = iSpanTop + 'px'
      }
    }
    $parent.onmouseleave = function () {
      spanArr.forEach((el) => {
        Velocity.animate(el, { top: iStartTop }, 500, 'spring')
        el.addEventListener('mouseenter', wordMouseEnterSpring)
        el.removeEventListener('mouseenter', wordMouseEnterCurrentIndex)
      })
      $parent.onmouseleave = null
      $parent.onmousemove = null
    }
  }
}
function wordMouseEnterCurrentIndex(e) {
  mouseEnterIndex = e.target.getAttribute('data-i')
}

function handleClick() {
  playPiano()
}

function initPiano() {
  audioIns = new Audio(piaonOgg)
}

function playPiano() {
  if (!audioIns) {
    initPiano()
    return
  }
  audioIns.currentTime = 0
  audioIns.play()
}


</script>

<template>
  <div :class="['list', reactiveData.initedAnimation ? 'animate' : '']" ref="ref_list">
    <li v-for="(item, index) in list" :key="index" :ref="'ref_list' + index">
      <a href="javascript:;" @click="handleClick">
        <span v-for="(word, i) in item.title" :key="'w_' + i" :data-i="i">{{word}}</span>
      </a>
    </li>
  </div>
</template>

<style lang="scss">
.list {
  padding: 20px 30px;
  li {
    list-style: none;
    text-align: left;
    height: 34px;
    a {
      display: inline-block;
      height: 100%;
      text-decoration: none;
      color: rgb(35, 117, 211);
      position: relative;
      cursor: default;
      span {
        font-size: 16px;
        line-height: 34px;
        height: 100%;
      }
    }
  }
  &.animate {
    li span {
      position: absolute;
      top: 0;
    }
  }
}
</style>
