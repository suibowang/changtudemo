<script setup lang="ts">
import * as PIXI from 'pixi.js'
import { Application, Sprite } from 'pixi.js';

const app = new Application<any>({
  width:window.innerWidth,
  height:window.innerHeight,
  backgroundColor:0x1099bb,
  resolution:window.devicePixelRatio||1,
})
document.body.appendChild(app.view)
//创建矩形
const rectangle = new PIXI.Graphics();
rectangle.lineStyle(4,0xff0000,1);
rectangle.beginFill(0x66ccff,1);//填充颜色,透明度
rectangle.drawRect(0,0,300,100);//位置大小
rectangle.endFill();//填充结束
//rectangle.scale.set(2,2);//图形缩放
//图形位移
//rectangle.position.set(200,200);
//图形旋转
//rectangle.rotation =0.5
//原点选择
//rectangle.pivot.set(150,100);
//设置边框样式
//矩形添加到舞台
//创建一个圆
app.stage.addChild(rectangle);
const circle = new PIXI.Graphics();
circle.beginFill(0x66ccff,1);
circle.drawCircle(300,300,32); 
circle.position.set(0,0);
circle.endFill();
app.stage.addChild(circle);
//创建一个纹理
const textture = PIXI.Texture.from("./2.png");    
//创建一个精灵
 const sprite = new PIXI.Sprite(textture);
 //设置精灵的锚点
 sprite.anchor.set(0.5,0.5)
 //设置精灵位置            
sprite.x = app.screen.width/2;
sprite.y = app.screen.height/2;
sprite.alpha = 0.5
app.stage.addChild(sprite);
//实现动画
app.ticker.add((dalta)=>{
  sprite.rotation +=0.01*dalta
})
//精灵添加交互事件
sprite.interactive = true;
sprite.on('click',()=>{
  console.log('click');
});
sprite.on("pointerenter",()=>{
  sprite.alpha = 1
});
sprite.on("pointerout",()=>{
  sprite.alpha = 0.5
})
</script>

<template>
<div>PIXI简单应用</div>
</template>

<style scoped>
/* canvas{
  width: 100vw;
  height: 100vh;
  position: fixed;
  background-color: black;
} */

</style>
