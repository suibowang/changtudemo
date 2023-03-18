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
//创建一个容器
const container = new PIXI.Container();
//添加资源
PIXI.Assets.addBundle("scene1",{
  tu1:"../imgs/图1.png",
  tu2:"../imgs/图2.png",
  tu3:"../imgs/图3.png",
  tu4:"../imgs/图4.png",
});
const assets =  PIXI.Assets.loadBundle("scene1",(progress)=>{
  console.log(progress)
});

//异步加载资源
//const texturePromise = PIXI.Assets.load(["tu1","tu2","tu3"]);
//创建加载后精灵
assets.then((textures)=>{
  //创建精灵
  const sprite = new Sprite(textures['tu1']);
  //设置精灵位置
  sprite.position.x = 100;
  sprite.position.y = 100;
  sprite.scale.set(0.5)
  //添加精灵
  //app.stage.addChild(sprite); 
  container.addChild(sprite);
  const sprite2 = new Sprite(textures['tu2']);
  //设置精灵位置
  sprite2.position.x = 300;
  sprite2.position.y = 300;
  sprite2.scale.set(0.5)
  //添加精灵
  //app.stage.addChild(sprite2); 
  container.addChild(sprite2);
  app.stage.addChild(container)
});


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
