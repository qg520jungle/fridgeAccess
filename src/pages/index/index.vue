<template>
  <div class="m-index" @click="clickHandle('test click', $event)">
    <div class="u-tit">冰箱小助手</div>
    <div class="m-body">
      这里设置冰箱大小
      <dl>
        <dt>冰箱门数</dt>
        <dd><input type="number" :value="nums" @change="changeNums"></dd>
      </dl>
      <dl>
        <dt>冰箱容量</dt>
        <dd><input type="text" v-model="caps"></dd>
      </dl>
      <div v-for="(item, index) in infoArr" :key="index">
        <dl>
          <dt>冰箱门功能</dt>
          <dd><input type="text" v-model="item.type"></dd>
        </dl>
        <dl>
          <dt>冰箱门大小</dt>
          <dd><input type="text" v-model="item.size"></dd>
        </dl>
      </div>
      
    </div>
    <div class="m-foot">
      <a href="/pages/mainCnt/main" class="u-btn u-btn-go">进入冰箱</a>
    </div>
  </div>
</template>

<script>
// import card from '@/components/setInit/page1'

export default {
  components: {
  },

  data () {
    return {
      title: '冰箱助手',
      nums: 0,
      caps: 0,
      infoArr: []
    }
  },

  computed: {
    // infoArr: {
    //   get () {
    //     let arr = []
    //     return arr
    //   },
    //   set () {

    //   }
    // }
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    },
    changeNums (e) {
      // console.log(e)
      // this.nums = 2
      console.log(this.nums)
      let newArr = []
      for (let i = 0; i < this.nums; i--) {
        if (i < this.infoArr.length) {
          newArr.push(this.infoArr[i])
        } else {
          let tempObj = {
            type: '',
            size: 0
          }
          newArr.push(tempObj)
        }
      }
      this.infoArr = newArr
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style lang="scss" scoped>
.m-index{
  background-color: rgb(185, 234, 238);
  height: 100vh;
  .u-tit{
    box-sizing: border-box;
    width: 100%;
    text-align: center;
    padding: 20px;
    font-size: 24px;
  }
}
</style>
