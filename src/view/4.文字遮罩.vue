<script setup lang="ts">
import * as PIXI from 'pixi.js'
import { Application, Sprite } from 'pixi.js';
import Pixi from '../view/1.pixi.vue';

const app = new Application<any>({
  width:window.innerWidth,
  height:window.innerHeight,
  backgroundColor:0x1099bb,
  resolution:window.devicePixelRatio||1,
})
document.body.appendChild(app.view)
//文字
const text = new PIXI.Text(
  "hello,word 王志祥",{
    fontFamily:'Arial',
    fontSize:50,
    fill:0xffffff,
    align:'center',
    //wordWrap:true,
   // wordWrapWidth:window.innerWidth,
  }
);
//创建一个圆
const circle = new PIXI.Graphics();
circle.beginFill(0x0000ff);
circle.drawCircle(app.screen.width/2,app.screen.height/2,200);
circle.endFill();
text.x=app.screen.width/2;
text.y=app.screen.height/2;
text.anchor.set(0.5);
//锚点
app.stage.addChild(text);
const bunny = PIXI.Sprite.from("../imgs/画面.jpg");
bunny.width =app.screen.width;
bunny.height =app.screen.height;
//使用文字作为精灵的遮罩
bunny.mask = circle
app.stage.addChild(bunny)
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
