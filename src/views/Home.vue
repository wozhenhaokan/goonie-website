<template>
  <div class="section" :style="{'height':offsetheight+'px'}">
    <div
      class="container"
      :style="{'transform': 'translate3d(0px,-'+ (fullPage*offsetheight+moveY) +'px, 0px)'}"
      @touchstart="touchstartevent($event)"
      @touchmove="touchmoveevent($event)"
      @touchend="touchendevent($event)">
      <div
        v-for="(i,index) in bannerList"
        :key="index"
        :style="{'height':offsetheight+'px','background-image':`url('${i.src}')`}">
        <!-- 主页 -->
        <div v-if="index === 0">
          <ul>
            <li><img src="../assets/img/logo.png" alt=""></li>
            <li style="font-size: 18px">
            <span
                    v-for="(item, childindex) in nav"
                    :key="childindex"
                    :class="{ac:childindex == activeIndex}"
                    @click="goto(childindex)"
            >{{ item.name }}</span>
            </li>
            <li style="font-size: 16px">咨询热线：13311552128</li>
          </ul>
          <transition name="title1_1">
            <p class="title" v-show="fullPage == 0">人工智能技术应用服务商<br>智慧网信解决方案提供商</p>
          </transition>
          <transition name="title1_2">
            <p class="transfer" v-show="fullPage == 0">提供数据采集、数据标引、数据治理、深度学习、<br>自然语言、知识图谱、可视化分析、人工智能为一体的方案</p>
          </transition>
          <img class="move_down" src="../../src/assets/img/move_down.png" alt="" v-show="fullPage == 0">
          <div>
            <span
              v-for="(item, index) in fullScreenDomList"
              :key="index"
              :style=item.style
              :class="{fullScreenAnimate: item.start}">
            </span>
          </div>
        </div>
        <!-- 谷尼舆情 -->
        <div v-if="index === 1" style="position: relative">
          <transition name="title">
            <img src="../assets/img/page2_logo.png" alt="" v-show="fullPage == 1">
          </transition>
          <transition name="title1_1">
            <p class="title" v-show="fullPage == 1">专注网络舆情12年，出版舆情著作4部</p>
          </transition>
          <transition name="title1_2">
            <p class="transfer" v-show="fullPage == 1">提供一套全流程化舆情服务体系，全面覆盖舆情监测-舆情分析-舆情预警-舆情处置-<br>
              舆情引导-新闻发布-传播评估-形象修复，管理舆情完整生命周期，实现舆情管理工作的系统化</p>
          </transition>
          <transition name="slide1">
            <img :src="i.content" alt="" v-show="fullPage == 1">
          </transition>
        </div>
        <!-- 智慧网信 -->
        <div v-if="index === 2">
          <transition name="title">
            <img src="../assets/img/page3_logo.png" alt="" v-show="fullPage == 2">
          </transition>
          <transition name="title1_1">
            <p class="title" v-show="fullPage == 2">
              智慧网信是基于大数据、云计算、人工智能技术建设的，<br>
              实现业务流程标准化、处理过程智能化、数据分析可视化的新型网信工作管理体系。
            </p>
          </transition>
          <transition name="slide1">
            <img :src="i.content" alt="" v-show="fullPage == 2">
          </transition>
        </div>
        <!-- 情报数据 -->
        <div v-if="index === 3">
          <transition name="title">
            <img src="../assets/img/page4_logo.png" alt="" v-show="fullPage == 3">
          </transition>
          <transition name="title1_1">
            <p class="title" v-show="fullPage == 3">
              防范企业风险  提升企业竞争力
            </p>
          </transition>
          <transition name="slide1">
            <img :src="i.content" alt="" v-show="fullPage == 3">
          </transition>
        </div>
        <!-- 业绩案例 -->
        <div v-if="index === 4">
          <transition name="title">
            <p class="title" v-show="fullPage === 4">客户案例</p>
          </transition>
          <transition name="slide1">
            <img src="../assets/img/page5_content1.png" v-show="fullPage === 4" alt="">
          </transition>
          <transition name="slide2">
            <img src="../assets/img/page5_content2.png" v-show="fullPage === 4" alt="">
          </transition>
          <transition name="slide3">
            <img src="../assets/img/page5_content3.png" v-show="fullPage === 4" alt="">
          </transition>
        </div>
        <!-- 联系我们 -->
        <div v-if="index === 5">
          <transition name="title">
            <p class="title" v-show="fullPage === 5">联系我们 <span class="title_in">（咨询有礼）</span></p>
          </transition>
          <transition name="title1_1">
            <div v-show="fullPage === 5">
              <p class="first_p">
                地       址：北京市海淀区清河嘉园甲1号楼A座14层<br>
                电 话：010-80812116 82834912 转分机804<br>
                手机/微信：133-1155-2128<br>
                邮箱：93742871@qq.com<br>
              </p>
              <img src="../assets/img/page6_content1.png" alt="" class="first_img">
            </div>
          </transition>
          <transition name="title1_2">
            <div v-show="fullPage === 5">
              <img src="../assets/img/page6_content2.png" class="second_img" alt="">
              <p class="second_p">《领导干部网络舆情工作指南》、《领导干部大数据应用<br>指南》书已被中国国家图书馆、中央党校图书馆、清华大<br>学图书馆、北京大学图书馆、复旦大学图书馆、同济大学<br>图书馆、浙江大学图书馆、厦门大学图书馆等近20所高校<br>图书馆收藏。</p>
            </div>
          </transition>
          <p class="footer">
            谷尼国际软件（北京）有限公司 版权所有 Copyright Gooniesoft Co.,Ltd All Rights Reserved<br>
            北京海淀公安分局备案号：1101085030 京ICP备09060067号
          </p>
        </div>
      </div>
    </div>
    <div class="fixed-list">
      <div v-for="(i,index) in bannerList" :key="index" :class="fullPage==index?'color':''" @click="pageInfo(index)">
      </div>
    </div>
  </div>
</template>
<script>
import page1 from '../assets/img/page1.jpg'
import page2 from '../assets/img/page2.jpg'
import page3 from '../assets/img/page3.jpg'
import page4 from '../assets/img/page4.jpg'
import page5 from '../assets/img/page5.jpg'
import page6 from '../assets/img/page6.jpg'
import page1Content from '../assets/img/page1_content.png'
import page2Content from '../assets/img/page2_content.png'
import page3Content from '../assets/img/page3_content.png'
import page4Content from '../assets/img/page4_content.png'
import page5Content from '../assets/img/page5_content1.png'
import page6Content from '../assets/img/page6_content1.png'
import fullScreenAnimate from './../../src/assets/js/fullScreenAnimate'
export default {
  data () {
    return {
      activeIndex: 0,
      fullScreenDomList: [
        {
          style: '',
          start: false
        }
      ],
      bannerList: [ // 盒子背景颜色
        {
          src: page1,
          content: page1Content
        },
        {
          src: page2,
          content: page2Content
        },
        {
          src: page3,
          content: page3Content
        },
        {
          src: page4,
          content: page4Content
        },
        {
          src: page5,
          content: page5Content
        },
        {
          src: page6,
          content: page6Content
        }
      ],
      nav: [
        {
          name: '主页',
          href: ''
        },
        {
          name: '谷尼舆情',
          href: ''
        },
        {
          name: '智慧网信',
          href: ''
        },
        {
          name: '情报数据',
          href: ''
        },
        {
          name: '业绩案例',
          href: ''
        },
        {
          name: '联系我们',
          href: ''
        }
      ],
      offsetheight: document.documentElement.clientHeight, // 获取当前页面的高度
      fullPage: 0, // 当前在第几页
      fullPageNum: false, // 是否在滑动
      startY: 0, // 手指落点
      moveY: 0, // 过度距离
      startTime: null // 开始触摸时间
    }
  },
  mounted () {
    // 阻止浏览器上下滑动默认行为
    document.body.addEventListener('touchmove', function (e) {
      e.preventDefault() // 阻止默认的处理方式(阻止下拉滑动的效果)
    }, { passive: false }) // passive 参数不能省略，用来兼容ios和android
    // 星星效果初始化
    this.fullScreenDomList = fullScreenAnimate.init()
    //
    // 在元素加载完毕的时候添加鼠标滑动事件
    //
    if (document.addEventListener) {
      document.addEventListener('DOMMouseScroll', this.scroll, false)
    }
    window.onmousewheel = document.onmousewheel = this.scroll

    var _this = this
    window.onresize = function () { // 定义窗口大小变更通知事件
      _this.offsetheight = document.documentElement.clientHeight
    }
  },
  watch: {
    fullScreenDomList () {
      setTimeout(() => {
        this.fullScreenDomList.map((item) => {
          item.start = true
        })
      }, 1000)
    }
  },
  methods: {
    /**
     * 导航跳转
     */
    goto (index) {
      this.fullPage = index
      this.activeIndex = index
    },
    //
    // 点击左侧小点时跳转到相应的page
    //
    pageInfo (index) {
      this.fullPage = index
      this.activeIndex = index
    },
    /**
     * 切换图片
     */
    showNext () { // 下一张
      if (this.fullPage >= (this.bannerList.length - 1)) {
        return false
      }
      this.fullPageNum = true
      this.pageInfo(this.fullPage + 1)
      //  css设置动画事件为500，所以等到500ms后滚动状态为false
      setTimeout(() => {
        this.fullPageNum = false
      }, 500)
    },
    showPrev () { // 上一张
      if (this.fullPage <= 0) {
        return false
      }
      this.fullPageNum = true
      this.pageInfo(this.fullPage - 1)
      setTimeout(() => {
        this.fullPageNum = false
      }, 500)
    },
    /**
     * 鼠标滚动事件
     */
    scroll (e) {
      this.activeIndex = 0
      e = e || window.event
      //
      // 是否正在滑动
      //
      if (this.fullPageNum) {
        return false
      }
      // e.wheelDelta为负数时向下滑动
      if (e.wheelDelta < 0) {
        this.showNext()
      } else {
        this.showPrev()
      }
    },
    /**
     * 手机滑屏组件
     */
    touchstartevent (e) {
      e.preventDefault()
      // 记录手指最开始的落点
      this.startY = e.changedTouches[0].clientY
      // console.log('开始')
    },
    touchmoveevent (e) {
      e.preventDefault()
      // 获取差值 自带正负
      var dx = e.changedTouches[0].clientY - this.startY
      this.moveY = (-dx)
      // console.log('进行中')
    },
    touchendevent (e) {
      e.preventDefault()
      // console.log('结束')
      // 在手指松开的时候，要判断当前是否滑动成功
      var dx = e.changedTouches[0].clientY - this.startY
      this.moveY = 0
      // 获取时间差
      var dTime = Date.now() - this.startTime
      // 滑动成功的依据是滑动的距离（绝对值）超过屏幕的三分之一 或者滑动的时间小于300毫秒同时滑动的距离大于30
      if (Math.abs(dx) > this.offsetheight / 5 || (dTime < 300 && Math.abs(dx) > 30)) {
        // 滑动成功了
        // 判断用户是往哪个方向滑
        if (dx > 0) {
          this.showPrev()
        } else {
          this.showNext()
        }
      }
    }
  }
}
</script>
<style lang="scss" scoped>
  $w-base: 1920;
  $h-base: 960;
  @function vh($value) {
    @return ($value / $h-base) * 100vh
  }
  @function vw($value) {
    @return ($value / $w-base) * 100vw
  }
  /* 专场效果*/
  /* 设置持续时间和动画函数 */
  .title-enter-active, .title-leave-active {
    transition: all 2s;
  }
  .title-enter, .title-leave-to {
    opacity: 0;
  }
  .title1_1-enter-active, .title1_1-leave-active {
    transition: all 1s cubic-bezier(.43,.46,.64,1.38);
  }
  .title1_1-enter, .title1_1-leave-to {
    opacity: 0;
    transform: translateX(-200px);
  }
  .title1_2-enter-active, .title1_2-leave-active {
    transition: all 1s cubic-bezier(.43,.46,.64,1.38);
  }
  .title1_2-enter, .title1_2-leave-to {
    opacity: 0;
    transform: translateX(200px);
  }

  .slide1-enter-active{
    transition: all 1s .4s;
  }
  .slide1-enter, .slide1-leave-to {
    opacity: 0;
    transform: translateY(-20px);
  }
  .slide1-leave-active {
    transition: all .5s;
  }

  .slide2-enter-active{
    transition: all 1s .7s;
  }
  .slide2-enter, .slide2-leave-to {
    opacity: 0;
    transform: translateY(-100px);
  }
  .slide2-leave-active {
    transition: all .5s;
  }

  .slide3-enter-active{
    transition: all 1s 1s;
  }
  .slide3-enter, .slide3-leave-to {
    opacity: 0;
    transform: translateY(-100px);
  }
  .slide3-leave-active {
    transition: all .5s;
  }

  .move_down{
    position: absolute;
    bottom: vh(40);
    animation: moveDownAnimate 1s ease-out infinite;
  }

  .section{
    overflow: hidden;
  }
  .container{
    width: 100%;height: 100%;
    position: relative; transform: translate3d(0px, 0px, 0px); transition: all 500ms ease;
    &>div{
      background-size: cover;
      background-position: center;
      position: relative;
      &>div{
        width: 1100px;
        margin: 0 auto;
      }
      &:nth-child(1)>div{
        ul{
          padding-top: 2vh;
          width: 1100px;
          margin: 0 auto;
          display: flex;
          justify-content: space-between;
          color: #fff;
          li{
            span{
              margin-right: 30px;
              display: inline-block;
              padding-bottom: 4px;
              cursor: pointer;

              &.ac{
                border-bottom: 1px solid #fff;
              }
            }
          }
        }
        .title{
          color: #fff;
          font-size: 32px;
          line-height: 54px;
          margin-bottom: 20px;
          margin-top: vh(300);
        }
        .transfer{
          color: #fff;
          font-size: 18px;
          line-height: 28px;
        }
      }
      &:nth-child(2)>div{
        img:first-child{
          height: 44px;
          margin: 0 auto;
          margin-top: vh(80);
        }
        .title{
          font-size: 18px;
          line-height: 28px;
          color: #fff;
          margin: vh(30) 0;
        }
        .transfer{
          font-size: 16px;
          line-height: 26px;
          color: #fff;
        }
        img:last-child{
          height: 250px;
          width: 640px;
          object-fit: contain;
          margin: 0 auto;
          margin-top: vh(80);
        }
      }
      &:nth-child(3)>div{
        img:first-child{
          height: 44px;
          margin: 0 auto;
          margin-top: vh(80);
        }
        .title{
          font-size: 16px;
          line-height: 28px;
          color: #fff;
          margin-top: vh(20);
        }
        img:last-child{
          height: auto;
          width: 700px;
          object-fit: contain;
          margin: 0 auto;
          margin-top: vh(60);
        }
      }
      &:nth-child(4)>div{
        img:first-child{
          height: 44px;
          margin: 0 auto;
          margin-top: vh(80);
        }
        .title{
          font-size: 18px;
          line-height: 28px;
          color: #fff;
          margin-top: vh(20);
        }
        img:last-child{
          height: 410px;
          width: auto;
          object-fit: contain;
          margin: 0 auto;
          margin-top: vh(40);
        }
      }
      &:nth-child(5)>div{
        padding-left: 30px;
        box-sizing: border-box;
        text-align: left;
        p{
          font-size: 32px;
          padding: vh(30) 0 vh(20);
          color: #fff;
        }
        img:nth-of-type(1){
          width: 1000px;
          object-fit: contain;
        }
        img:nth-of-type(2){
          margin: vh(14) 0;
          width: 914px;
          object-fit: contain;
        }
        img:nth-of-type(3){
          width: 416px;
          object-fit: contain;
        }
      }
      &:nth-child(6)>div{
        padding-left: 30px;
        box-sizing: border-box;
        text-align: left;
        .title{
          color:#fff;
          font-size: 28px;
          padding: vh(30) 0 vh(20);
        }
        .title_in{
          font-size: 20px;
          color: #ffc600
        }
        &>div{
          display: flex;
          width: 915px;
          justify-content: space-between;
        }
        .first_p{
          font-size: 16px;
          line-height: vh(36);
          color: #fff;
        }
        .second_p{
          margin-right: -60px;
          width: 415px;
          font-size: 16px;
          line-height: 30px;
          color: #fff;
          padding-top: 100px;
          transform: translateX(-40px);
        }
        img{
          object-fit: contain;
        }
        .first_img{
          width: 119px;
          height: 119px;
        }
        .second_img{
          width: 500px;
          height: 380px;
        }
        .footer{
          position: absolute;
          bottom: 20px;
          font-size: 16px;
          width: 1100px;
          margin: 0 auto;
          text-align: center;
          color: #fff;
        }
      }
    }
  }
  .fixed-list{
    position: fixed;
    top: 50%;
    right: 5%;
    height: 190px;
    width: 15px;
    flex-direction: column;
    transform: translateY(-50%);
    display: flex;
    justify-content: space-between;
    div{
      width: 15px;
      height: 15px;
      border: 1px solid #fff;
      border-radius: 50%;
    }
    div.color{
      background:#9fabdf;
    }
  }
</style>
<style>
  @keyframes fullScreenAnimate
  {
    100% {top:0}
  }

  @-webkit-keyframes fullScreenAnimate /* Safari 与 Chrome */
  {
    100% {top:0}
  }

  @keyframes moveDownAnimate
  {
    0% {transform:translateY(0px)}
    50% {transform:translateY(10px)}
    100% {transform:translateY(0px)}
  }

  @-webkit-keyframes moveDownAnimate /* Safari 与 Chrome */
  {
    0% {transform:translateY(0px)}
    50% {transform:translateY(10px)}
    100% {transform:translateY(0px)}
  }
</style>
