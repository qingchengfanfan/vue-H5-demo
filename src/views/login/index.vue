<!-- 绑定手机 -->
<template>
    <div id="bindMobile">
        <h4>登录</h4>
        <div class="input_div phone">
            <div class="area_code">+86</div>
            <input type="tel" placeholder="请输入手机号">
            <div class="get_code">获取验证码</div>
        </div>
        <div class="input_div msg_code">
            <div class="area_code">验证码</div>
            <input type="tel" placeholder="请输入手机号">
        </div>
        <div class="bind" :class='{active: active}'>登录</div>
    </div>
</template>

<script>
import { tips, wxAuthorize } from 'base/global/g'
import { isWX } from 'base/global/tools'
import { Indicator } from 'mint-ui'
export default {
    data() {
        return {
            active: false // 登录按钮的样式
        }
    },
    components: {
    },

    computed: {},
    beforeRouteEnter(to, from, next) {
        Indicator.open({
            text: '请稍后...',
            spinnerType: 'double-bounce'
        })
        // ...
        if (isWX) {
            if (to.query.code) {
                // todo
                // 调用后端的接口去实现微信登录
            } else {
                // 去授权
                wxAuthorize(window.location.origin + window.location.pathname)
            }
        } else {
            Indicator.close()
            next()
        }
    },
    mounted() {
        tips({
            message: '111222333'
        }).then(() => {
            tips({
                message: '444555666'
            })
        })
    },

    methods: {}
}

</script>
<style lang='scss' scoped>
#bindMobile {
  overflow: hidden;
  h4 {
    width: 292px;
    height: 81px;
    opacity: 1;
    font-size: 58px;
    color: rgba(51, 51, 51, 1);
    line-height: 81px;
    letter-spacing: 0.28px;
    margin: 56px 0 68px 32px;
  }
  .input_div {
    width: 686px;
    height: 78px;
    opacity: 1;
    margin: 0 auto;
    border-bottom: 1px solid #eeeeee; /* no */
    display: flex;
    justify-content: flex-start;
    margin-top: 34px;
    .area_code {
      width: 130px;
      border-right: 1px solid #979797; /* no */
      height: 48px;
      font-size: 34px;
      color: rgba(54, 54, 54, 1);
      line-height: 48px;
    }
    input {
      display: block;
      width: 226px;
      height: 48px;
      border: none;
      font-size: 34px;
      margin-left: 40px;
      margin-right: 147px;
      -webkit-tap-highlight-color: transparent;
      -webkit-appearance: none;
      &::-webkit-input-placeholder {
        color: #bdbdbd;
        font-size: 34px;
      }
      &:focus {
        border-bottom: none; /* no */
        box-shadow: none; /* no */
      }
    }
    .get_code {
      width: 143px;
      height: 48px;
      font-size: 28px;
      color: #f43231;
      line-height: 48px;
    }
  }
  .bind {
    width: 686px;
    height: 88px;
    background: #acacac;
    margin: 72px auto 0;
    border-radius: 8px;
    text-align: center;
    line-height: 88px;
    color: #fff;
    font-size: 36px;
    &.active {
      background-image: linear-gradient(left, #ff7453, #f43231);
    }
  }
}
</style>
