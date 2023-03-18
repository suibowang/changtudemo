<script setup lang="ts">
import * as PIXI from 'pixi.js'
import { Application, Sprite } from 'pixi.js';
import {OutlineFilter,GlowFilter} from 'pixi-filters'

const app = new Application<any>({
  width:window.innerWidth,
  height:window.innerHeight,
  backgroundColor:0x1099bb,
  resolution:window.devicePixelRatio||1,
});
document.body.appendChild(app.view);
//创建一个纹理
const textture = PIXI.Texture.from("./imgs/玩计划.png");
//创建一个精灵
const sprite = new Sprite(textture);
sprite.anchor.set(0.5);
sprite.position.set(window.innerWidth/2,window.innerHeight/2);
app.stage.addChild(sprite);
//创建模糊滤镜
const blurFilter = new PIXI.BlurFilter();
blurFilter.blur = 10;
//sprite.filters = [blurFilter]
// //监听鼠标指针是否进入
// sprite.interactive = true;
// sprite.on("pointerover",()=>{
//   blurFilter.blur = 0
// })
// //监听鼠标是否离开
// sprite.on("pointerout",()=>{
//   blurFilter.blur = 10
// })
//创建轮廓滤镜
const outlineFilter = new OutlineFilter(5,0xffff00);
const glowFilter = new GlowFilter({
  color:0xff0000,
  distance:15,
  outerStrength:5,
  innerStrength:0,
  quality:0.5,
  
});
sprite.filters = [outlineFilter,glowFilter];
</script>
<template>
<div id='a'></div>
</template>

<style scoped>
/* canvas{
  width: 100vw;
  height: 100vh;
  position: fixed;
  background-color: black;
} */

</style>
