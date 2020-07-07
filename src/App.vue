<template>
    <div class="container" @mouseenter="stop" @mouseleave="go">
        <ul class="wrap"  :style="containerStyle">
            <li v-for="(item,index) in sliders" :key="index">
                <img class="img" :src="item.img" alt="">
            </li>
        </ul>
        <ul class="dot">
            <li v-for="(index) in sliders.length" :class="{'active':index===currentIndex+1}" @mouseover="change(index)">{{index}}</li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'slider',
        data () {
            return {
                sliders:[
                    {
                        img:require('./images/1.jpg')
                    },
                    {
                        img:require('./images/2.jpg')
                    },
                    {
                        img:require('./images/3.jpg')
                    },
                    {
                        img:require('./images/4.jpg')
                    },
                    {
                        img:require('./images/5.jpg')
                    }
                ],
                currentIndex:0,
                timer:null,
                initialInterval:5
            }
        },
        computed:{
            containerStyle(){  //这里用了计算属性，用transform来移动整个图片列表
                return {
                    transform:`translate3d(${this.currentIndex*-600}px, 0, 0)`
                }
            },
        },
        created() {
            //在DOM加载完成后，下个tick中开始轮播
            this.$nextTick(() => {
                this.timer = setInterval(() => {
                    this.play()
                }, 2000)
            })
        },
        methods:{
            play(){
                this.currentIndex++;
                if (this.currentIndex > this.sliders.length - 1) {
                    this.currentIndex = 0
                }
                //console.log(this.currentIndex);
            },
            go(){
                this.timer = setInterval(() => {
                    this.play()
                }, 2000)
            },
            stop() {
                clearInterval(this.timer)
                this.timer = null
            },
            change(dotIndex){
                //console.log(dotIndex);
                this.currentIndex=dotIndex-1;
            }
        }
    }
</script>
