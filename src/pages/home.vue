<template>
  <view id="home" class="clearfix">
    <view id="local">
      <view>
        <p><van-icon name="location-o" />中国<van-icon name="arrow" id="localindex"/></p>
      </view>
    </view>
    <view id="menulist">
      <view id="pointsearch" @click="out">
        <van-search
        v-model="pointword"
        shape="round"
        background="rgba(0,0,0,0)"
        placeholder="请输入搜索关键词"
      />
      </view>
      <view id="searchlist">
        <view v-for="(item,index) in searchList" :key="item+index">{{item}}</view>
      </view>
      <view id="variouslist">
        
      </view>
      <view id="lunboAd" class="clearfix">
        <image src="../static/ad1.png" alt="" class="img" :style="img1">
        <image src="../static/ad2.png" alt="" class="img" :style="img2">
      </view>
    </view>
  </view>
</template>
<script>
export default {
  data () {
    return {
      pointword: '',
      searchList: ['刀削面','麻辣烫','奶茶','炸鸡'],
      top:{
        img1:'top:0;z-index:999;', 
        img2:'top:calc(10vh);z-index:99;'
      },
      isScroll: false,
      firstIn: false
    }
  },
  computed: {
    img1: function () {
      return this.top.img1
    },
    img2: function () {
      return this.top.img2
    }
  },
  onReady () {
    this.lunbo()
  },
  onShow () {
    if (this.isScroll === true) {
      uni.setTabBarItem({
        index: 0,
        text: '回顶部',
        iconPath: '/static/home.png',
        selectedIconPath: '/static/back.png'
      })
    }
  },
  onHide () {
    uni.setTabBarItem({
      index: 0,
      text: '首页',
      iconPath: '/static/home.png',
      selectedIconPath: '/static/homeSelect.png'
    })
    this.firstIn = true
  },
  onPageScroll (obj) {
    if (obj.scrollTop !== 0) {
      uni.setTabBarItem({
        index: 0,
        text: '回顶部',
        iconPath: '/static/home.png',
        selectedIconPath: '/static/back.png'
      })
    } else {
      uni.setTabBarItem({
        index: 0,
        text: '首页',
        iconPath: '/static/home.png',
        selectedIconPath: '/static/homeSelect.png'
      })
    }
    this.isScroll = true
  },
  onTabItemTap (e) {
    let san = e.index
    let name = e.text
    if (san == 0 && this.firstIn === false) {
      uni.pageScrollTo({
        scrollTop: 0,
        complete () {
          uni.setTabBarItem({
            index: 0,
            text: '首页',
            iconPath: '/static/home.png',
            selectedIconPath: '/static/homeSelect.png'
          })
        }
      })
    } else {
      this.firstIn = false
    }
  },
  methods: {
    out () {
      console.log('hhh')
      uni.navigateTo({
        url: 'menuSearch'
      })
    },
    lunbo () {
      setInterval(() => {
        for (let i in this.top) {
          if (this.top[i] == 'top:calc(10vh);z-index:99;') {
            this.top[i] = 'top:0;z-index:999;'
          } else if(this.top[i] == 'top:0;z-index:999;') {
            this.top[i] = 'top:calc(-10vh);z-index:99;'
          }
        }
        setTimeout(() => {
          for (let i in this.top) {
            if (this.top[i] == 'top:calc(-10vh);z-index:99;') {
              this.top[i] = 'top:calc(10vh);z-index:99;'
            }
          }
        },500)
      },1000)
    }
  }
}
</script>
<style scoped>
#home{
  width: 750rpx;
  height: calc(100vh);
  background: linear-gradient(to right, rgb(255, 221, 77), rgb(255, 210, 77), rgb(255, 198, 77));
}
#local{
  display: flex;
  align-items: center;
  margin-top: calc(5vh);
  margin-left: 5px;
  margin-bottom: calc(1vh);
}
#localindex{
  font-size: .5em;
  font-style: bold;
  border-radius: 20%;
  box-sizing: border-box;
}
#menulist{
  width: 750rpx;
  height: calc(95vh);
  border-radius: 25px 25px 0 0;
  background: linear-gradient(to bottom,rgb(252, 252, 253), rgb(245, 245, 246));
  box-sizing: border-box;
  overflow: hidden;
  margin:0 auto;
}
#searchlist{
  margin-left: calc(2vw);
  margin-top: 0;
  display:flex;
  align-items: center;
}
#searchlist>view{
  display:inline-block;
  font-size: .5em;
  width: calc(10vw);
  background-color: rgb(245, 245, 246);
  border-radius: 25px;
  margin-left: calc(2vw);
  text-align: center;
}
#variouslist{
  width: calc(90vw);
  height: calc(40vh);
  background-color: #fff;
  margin: calc(2vh) auto;
  border-radius: 10px;
}
#lunboAd{
  width: calc(95vw);
  margin: calc(2vh) auto;
  height: calc(10vh);
  overflow:hidden;
  position: relative;
}
#lunboAd image{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  transition: 0.5s;
}
</style>