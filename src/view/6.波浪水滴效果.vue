<script setup lang="ts">
import * as PIXI from 'pixi.js'
import { Application, DisplacementFilter, Sprite, } from 'pixi.js';
import {OutlineFilter,GlowFilter,ShockwaveFilter} from 'pixi-filters'

const app = new Application<any>({
  width:window.innerWidth,
  height:window.innerHeight,
  backgroundColor:0x1099bb,
  resolution:window.devicePixelRatio||1,
});
document.body.appendChild(app.view);
//创建一个纹理
const texture = PIXI.Texture.from('./imgs/画面.jpg');
//创建一个精灵
const sprite = new Sprite(texture);
sprite.width=app.screen.width;   
sprite.height=app.screen.height;
//创建容器
const container = new PIXI.Container();
//添加精灵到容器
container.addChild(sprite);
app.stage.addChild(container);
//添加文字
const text = new PIXI.Text('Hello Pixi.js', {
  fontFamily:'Arial',
  fontSize:100,
  fill:'white',
  align:'center',
  //wordWrap:true, 空格换行
  dropShadow:true,
  dropShadowColor:'#ff0000',//阴影颜色
  dropShadowAngle:Math.PI/2,
  dropShadowDistance:5,//阴影大小
  dropShadowBlur:4,//阴影模糊度
});
text.x=app.screen.width/2;
text.y=app.screen.height/2;
text.anchor.set(0.5);
container.addChild(text);

//添加置换滤镜
const displancementSprite = PIXI.Sprite.from("./imgs/12.webp");
displancementSprite.scale.set(5);
displancementSprite.texture.baseTexture.wrapMode = PIXI.WRAP_MODES.REPEAT;
const displacementFilter = new PIXI.DisplacementFilter(displancementSprite);
container.addChild(displancementSprite)


//水波纹滤镜
const shockwaveFilter = new ShockwaveFilter([
  Math.random()*app.screen.width,
  Math.random()*app.screen.height,
],{
  radius:100,//半径
  wavelength:40,//波长
  amplitude:55,//振幅
  speed:200//速度

});
const shockwaveFilter2 = new ShockwaveFilter([
  Math.random()*app.screen.width,
  Math.random()*app.screen.height,
],{
  radius:100,//半径
  wavelength:40,//波长
  amplitude:80,//振幅
  speed:200//速度

});
const shockwaveFilter3 = new ShockwaveFilter([
  Math.random()*app.screen.width,
  Math.random()*app.screen.height,
],{
  radius:100,//半径
  wavelength:45,//波长
  amplitude:100,//振幅
  speed:200//速度

});
container.filters=[displacementFilter,shockwaveFilter,shockwaveFilter2,shockwaveFilter3];
app.ticker.add((delta)=>{
  displancementSprite.x += 1;
  displancementSprite.y += 1;
  createWave(shockwaveFilter,1);
  createWave(shockwaveFilter2,1.2);
  createWave(shockwaveFilter3,0.7);
});

function createWave(waveFilter:any,resetTime:any){
  waveFilter.time +=0.01;
  if(waveFilter.time>resetTime){
  waveFilter.time=0;
  waveFilter.center = [
    Math.random()*app.screen.width,
    Math.random()*app.screen.height,
  ]
  }

}
//监听点击事件
app.view.addEventListener("click",(e:any)=>{
  console.log(e.clientX,e.clientY)
  shockwaveFilter3.center=[e.clientX,e.clientY];
  shockwaveFilter3.time=0;
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
