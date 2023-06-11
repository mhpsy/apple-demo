<script setup>
import {onMounted, ref} from "vue";

const handleClickBox = (e) => {
    // console.log(e)
    // if (videoDom.value) {
    //     console.log(videoDom.value.currentTime)
    // }
}


const videoDom = ref(null);
const videoDom2 = ref(null);
const videoDom3 = ref(null);
const lastScrollTop = ref(0);
const windowScroll = (e) => {
    let scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
    if (scrollTop > lastScrollTop.value) {
        handleVideo(videoDom, '+')
        if (isInViewPortWithPx(videoDom2.value)) {
            handleVideo(videoDom2, '+')
        }
        // videoDom3.value.currentTime = handleVideoCurrentTime(videoDom3)
    } else {
        handleVideo(videoDom, '-')
        if (isInViewPortWithPx(videoDom2.value)) {
            handleVideo(videoDom2, '-')
        }
        // videoDom3.value.currentTime = handleVideoCurrentTime(videoDom3)
    }
    lastScrollTop.value = scrollTop;

    console.log(isInViewPort(videoDom2.value))
}

//防抖 用不到了
const debounce = (fn, delay = 500) => {
    let timer = null;
    return (...args) => {
        if (timer) {
            clearTimeout(timer);
        }
        timer = setTimeout(() => {
            fn(...args);
        }, delay)
    }
}


//控制视频播放
const handleVideo = (dom, symbol, step = 0.1) => {
    let realDom = dom.value || dom;
    if (realDom) {
        if (symbol === '+') {
            realDom.currentTime += step;
        } else {
            realDom.currentTime -= step;
        }
    }
}

//判断元素是否在可视区域
const isInViewPort = (dom) => {
    let realDom = dom.value || dom;
    if (realDom) {
        let rect = realDom.getBoundingClientRect();
        let top = rect.top;
        let bottom = rect.bottom;
        let height = rect.height;
        return top + height > 0 && bottom - height < window.innerHeight;
    }
    return false;
}

// const handleVideoCurrentTime = (dom) => {
//     let realDom = dom.value || dom;
//     if (realDom) {
//         const rect = realDom.getBoundingClientRect();
//         const scrollTop = window.pageYOffset; //滚动条距离顶部高度
//         const boxPosition = scrollTop - (top - window.innerHeight)
//         if (boxPosition <= 0) return 0 //未达到可视位置时不执行以下
//         return (boxPosition - window.innerHeight) / rect.height * realDom.currentTime
//     }
//     return 0;
// }


const isInViewPortWithPx = (dom, px = 100) => {
    let realDom = dom.value || dom;
    if (realDom) {
        let rect = realDom.getBoundingClientRect();
        let top = rect.top;
        let bottom = rect.bottom;
        let height = rect.height;
        return top + height > px && bottom - height < window.innerHeight - px;
    }
    return false;
}

window.addEventListener('scroll', windowScroll)

onMounted(() => {
    console.log(videoDom.value)
})
</script>

<template>
    <video class="video1" ref="videoDom" src="@/assets/large.webm"/>
    <div class="box" @click="handleClickBox">
        <div class="item" v-for="i in 25">{{ i }}</div>
    </div>
    <video class="video2" ref="videoDom2" src="@/assets/large.webm"/>
    <video class="video3" ref="videoDom3" src="@/assets/large.webm"/>
</template>


<style scoped>
.video1 {
    position: fixed;
    top: 100px;
    left: 50%;
    transform: translateX(-50%);
    width: 500px;
}

.video2 {

}

.box {
    .item {
        height: 100px;
    }
}
</style>
