<script setup lang="ts">
import { ref, onMounted } from 'vue';
import * as PIXI from 'pixi.js';
import { Application, DisplacementFilter, Sprite, } from 'pixi.js';
import AlloyTouch from 'alloytouch';
//import { gsap } from 'gsap'
let w = document.body.clientWidth;
let h = document.body.clientHeight;
let min = (w < h) ? w : h;
let scale = min / 750;
console.log(w, h, min, "放大系数：", scale);
const app = new Application<any>({
  width: w,
  height: h,
  backgroundColor: 0x1099bb,
  //resolution: window.devicePixelRatio || 1,
});
//创建容器
const container = new PIXI.Container();
container.width = 4250;
container.height = 375;
container.x = 0;
app.stage.addChild(container);
PIXI.Assets.addBundle("scene1", {
  tu1: "../imgs/背景.jpg",
});
const assets = PIXI.Assets.loadBundle("scene1", (progress) => {
  console.log("123456")
});
document.body.appendChild(app.view);
assets.then((textures) => {
  //添加背景精灵
  const sprite = new Sprite(textures.tu1);
  sprite.width = 4250;
  sprite.height = 375;
  sprite.position.set(0, 0);
  sprite.scale.set(1);
  container.addChild(sprite);
  app.stage.addChild(container)
})
app.stage.scale.set(scale, scale);
app.stage.rotation = 1.57;
app.stage.pivot.set(0.5);
app.stage.x = w;
onMounted(()=>{
  function initTouch(vertical: any, val: any) {
  let max = (w > h) ? w : h;
  let scrollDis = app.stage.width - max
  console.log(app.stage.width,max)
  const alloyTouch = new AlloyTouch({
    touch: "body",//反馈触摸的dom
    vertical: vertical,//不必需，默认是true代表监听竖直方向touch
    // target: { y: 0 }, //运动的对象
    // property: "y",  //被运动的属性
    min: -3500, //不必需,运动属性的最小值
    max: 0, //不必需,滚动属性的最大值
    // sensitivity: 1,//不必需,触摸区域的灵敏度，默认值为1，可以为负数
    // factor: 1,//不必需,表示触摸位移运动位移与被运动属性映射关系，默认值是1
    // moveFactor: 1,//不必需,表示touchmove位移与被运动属性映射关系，默认值是1
    // step: 45,//用于校正到step的整数倍
    bindSelf: false,
    maxSpeed: 1, //不必需，触摸反馈的最大速度限制 
    value: 0,
    initialValue: 0,
    change: function (value: any,) {
      //console.log(min)
      app.stage.position[val] = value;
      console.log(app.stage.position[val])
     
    },
    // touchStart: function (evt, value) { },
    //   touchMove: function (evt, value) { },
    //   touchEnd: function (evt, value) { },
    //   tap: function (evt, value) { },
    //   pressMove: function (evt, value) { },
    //   animationEnd: function (value) { } //运动结束

  }
  )
}
initTouch(true, 'y');
})

</script>


<template>
  <div>
  </div>
</template>

<style scoped>
.abc {
  width: 100vw;
  height: 100vh;
}
</style>
