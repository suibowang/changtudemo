<script setup lang="ts">
import * as PIXI from 'pixi.js'
import { Application, DisplacementFilter, Sprite, } from 'pixi.js';
import { OutlineFilter, GlowFilter, ShockwaveFilter } from 'pixi-filters'
//import AlloyTouch from 'alloytouch'

const app = new Application<any>({
  width: window.innerWidth,
  height: window.innerHeight,
  backgroundColor: 0x1099bb,
  resolution: window.devicePixelRatio || 1,
});
document.body.appendChild(app.view);
//创建容器
const container = new PIXI.Container();
app.stage.addChild(container);
//添加整个恐龙纹理
const baseTexture = PIXI.BaseTexture.from("./imgs/game.png");
//创建恐龙精灵纹理
const dinoTexture = new PIXI.Texture(
  baseTexture,
  new PIXI.Rectangle(75, 0, 88, 100) //长方形
);
//创建恐龙精灵
const dino = new Sprite(dinoTexture);
dino.visible = false;//初始不显示恐龙
container.addChild(dino);
//恐龙跑步动画
const runTextures = []
for (let i = 0; i < 2; i++) {
  runTextures.push(
    new PIXI.Texture(
      baseTexture,
      new PIXI.Rectangle(1680 + (2 + i) * 88, 0, 82, 100) //长方形
    )
  );
};
const runAnimation = new PIXI.AnimatedSprite(runTextures);
runAnimation.animationSpeed = 0.1;
runAnimation.play();
runAnimation.visible = false
container.addChild(runAnimation);

//恐龙跳跃精灵
const jumpTexture = new PIXI.Texture(
  baseTexture,
  new PIXI.Rectangle(1680 + 88, 0, 82, 100) //长方形
);
const jumpSprite = new PIXI.Sprite(jumpTexture);
jumpSprite.x = 60;
jumpSprite.y =0;
//jumpSprite.y = window.innerHeight - 180
//jumpSprite.visible = false;
console.log("123",window.innerHeight - 180)
container.addChild(jumpSprite);
console.log("222",jumpSprite.y)
//创建地面精灵
const groundTexture = new PIXI.Texture(
  baseTexture,
  new PIXI.Rectangle(50, 100, 2300, 30) //长方形
);
const groundSprite = new PIXI.TilingSprite(groundTexture);//平铺
groundSprite.width = window.innerWidth;
groundSprite.height = 30;
//设置地面精灵的位置
groundSprite.position.set(0, window.innerHeight - 100);
container.addChild(groundSprite);
//创建仙人掌精灵
const catusTexture = new PIXI.Texture(
  baseTexture,
  new PIXI.Rectangle(515, 0, 33, 80) //长方形
);
const catusSprite = new PIXI.Sprite(catusTexture);//平铺
catusSprite.x = window.innerWidth / 2;
catusSprite.y = window.innerHeight - 60 - 100;
container.addChild(catusSprite)

//创建文字
let startText = new PIXI.Text("开始游戏", {
  fontFamily: 'Arial',
  fontSize: 30,
  fill: 0xffffff,
  align: 'center'
});
startText.x = window.innerWidth / 2;
startText.y = window.innerHeight / 2;
startText.anchor.set(0.5)
container.addChild(startText);
//开始点击事件监听
startText.interactive = true
startText.on("click", () => {
  playGame();
})
let isGameing = false

//开始游戏函数

function playGame() {
  isGameing = true;
  runAnimation.visible = true;
  runAnimation.x = 60;
  runAnimation.y = window.innerHeight - 185;
  startText.visible =false;
  //jumpSprite.visible =true;
  console.log("开始游戏")
};

//游戏得分
let score = 0
//跳跃速度
let jumpVelocity = 20;
//初始化重力
let gravity = 1;
//游戏结束
let isGameover = false

//游戏循环
app.ticker.add((delta) => {
  if(isGameover)
  return
  if (isGameing) {
    //地面移动
    groundSprite.tilePosition.x -= 10;
    //仙人掌移动
    catusSprite.x -= 10
    if (catusSprite.x < -30) {
      catusSprite.x = window.innerWidth;
      score++;
    }
  }
  //跳跃复原
  if (jumpSprite.visible) {
   // console.log(jumpSprite.y)
    jumpVelocity -= gravity;//20 19 18 17 16 15 14 13
    jumpSprite.y -= jumpVelocity;//-20 -19- 18
    console.log(jumpVelocity, jumpSprite.y)
    if (jumpSprite.y > window.innerHeight - 180) { 
      jumpSprite.y = window.innerHeight - 180;
      jumpVelocity = 20;
      jumpSprite.visible = false;
      runAnimation.visible = true;
    }
  }
  //检测碰撞
  if (jumpSprite.y > catusSprite.y - 80 && catusSprite.x < jumpSprite.x + 60 && catusSprite.x > jumpSprite.x - 60) {
    console.log("游戏结束")
    gameOver();
    startText.visible =false;
    let overText = new PIXI.Text("游戏结束，最后得分："+score,{
      fontFamily: 'Arial',
      fontSize: 30,
      fill: 0xffffff,
      align: 'center'
    });
    overText.x = window.innerWidth / 2;
    overText.y = window.innerHeight / 2;
    overText.anchor.set(0.5)
    overText.visible =true;
    container.addChild(overText);
    overText.interactive = true;
    overText.on("click", () => {
      location.reload();
    })

  }
});
function gameOver(){
  isGameover =true
}
window.addEventListener('keydown', (e) => {
  if (e.code === "Space") {
    console.log("跳跃");
    runAnimation.visible = false;
    jumpSprite.visible = true;
    jumpVelocity = 20;
    console.log(jumpSprite.y)
  }
})
// const alloytouch = new AlloyTouch({
//   touch: "body", // 反馈触摸的dom
//     vertical: , // 不必需，默认是true代表监听竖直方向touch
//     min: -scrollDis, // 不必需,运动属性的最小值
//     maxSpeed: 1,
//     max: 0, // 不必需,滚动属性的最大值
//     bindSelf: false,
//     initialValue: 0,
// })
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
