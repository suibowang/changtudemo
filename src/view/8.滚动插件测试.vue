<template>
    <div class="abc" id="aaa">
        <img src="imgs/背景.jpg" alt="" class="a">
    </div>
</template>
<script setup lang='ts'>
import { ref, reactive, onActivated, onMounted } from 'vue';
import AlloyTouch from 'alloytouch';

onMounted(() => {   //生命周期挂载之后
    let ads = document.getElementById('aaa')
    console.log("456", ads);
    const ddd = new AlloyTouch({
        touch: ads,//反馈触摸的dom
        vertical: false,//不必需，默认是true代表监听竖直方向touch
        target: { x: 0 }, //运动的对象
        property: "x",  //被运动的属性
        min: 100, //不必需,运动属性的最小值
        max: 2000, //不必需,滚动属性的最大值
        sensitivity: 1,//不必需,触摸区域的灵敏度，默认值为1，可以为负数
        factor: 1,//不必需,表示触摸位移运动位移与被运动属性映射关系，默认值是1
        moveFactor: 1,//不必需,表示touchmove位移与被运动属性映射关系，默认值是1
        step: 45,//用于校正到step的整数倍
        bindSelf: false,
        maxSpeed: 2, //不必需，触摸反馈的最大速度限制 
        value: 0,
        change: function (value:any,target:any) {
            console.log(value)
            target.style.transform = "translate(0," + value + "px)"
            target.style.webkitTransform = "translate(0," + value + "px)"
        },
        touchStart: function (evt, value) { },
        touchMove: function (evt, value) { },
        touchEnd: function (evt, value) { },
        tap: function (evt, value) { },
        pressMove: function (evt, value) { },
        animationEnd: function (value) { } //运动结束
    })
})

</script>
<style scoped>
.abc {
    width: 100vw;
    height: 100vh;
    background-color: blanchedalmond;
    position: absolute;


}

.a {
    width: 4250px;
    height: 375px;
    background-color: red;
    /* position: absolute; */
    left: 0;
    top: 0;

}
</style>