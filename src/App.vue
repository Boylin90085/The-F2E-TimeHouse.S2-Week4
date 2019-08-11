<template>
  <div id="app">
    <div class="container">
      <div class="row d-flex justify-content-center">
        <div class="col-sm-6 m-progress-bar">
          <div class="m-progress-bar__item">
            <div class="m-progress-bar__icon m-progress-bar__icon--active">
              <i class="far fa-user"></i>
            </div>
            <p>
              填寫資料
            </p>
          </div>
          <div class="m-progress-bar__line"></div>
          <div class="m-progress-bar__item">
            <div class="m-progress-bar__icon">
              <i class="fas fa-dollar-sign"></i>
            </div>
            <p>
              選擇付款方式
            </p>
          </div>
          <div class="m-progress-bar__line"></div>
          <div class="m-progress-bar__item">
            <div class="m-progress-bar__icon">
              <i class="far fa-credit-card"></i>
            </div>
            <p>
              前往付款
            </p>
          </div>
        </div>
      </div>
      <div class="row align-items-start">
        <div class="order-info col-sm-4" :class="{ open: orderOpen }">
          <span class="order-info__name" @click="orderOpen = !orderOpen">
            訂 單 資 訊
          </span>
          <img src="./image/commodity 2x.png" alt="">
          <h4 class="order-info__title">
            玩具解剖展｜夜間加場：紐約街頭潮 玩派對 Special Guest DJ RayRay
          </h4>
          <p>
            2019-08-09(五) 19:30 ~ 21:00 (GMT+8)
          </p>
          <p>
            台灣台北市中正區八德路一段1號
          </p>
          <p>
            訂單編號：1908020833432821107310
          </p>
          <p class="order-info__price">
            總價：1688元
          </p>
        </div>
        <div class="form__container col-sm-8 col-12">
          <h3 class="form__title">
            <strong>
              Step.1
            </strong>
            <span>
              填寫聯絡人資訊
            </span>
          </h3>
          <div class="row">
            <div class="col-sm-6">
              <div class="form-group">
                <label class="form__require" for="name">姓名</label>
                <input
                  v-validate="'required'"
                  v-model="name"
                  name="name"
                  type="text"
                  class="form-control"
                  id="name">
              </div>
            </div>
            <div class="col-sm-6">
              <div class="form-group">
                <label class="form__require" for="phone">行動電話</label>
                <input
                  v-validate="'required|numeric'"
                  v-model="phone"
                  name="phone"
                  type="tel"
                  class="form-control"
                  id="phone">
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-sm-6">
              <div class="form-group">
                <label class="form__require" for="email">電子郵件</label>
                <input
                  v-validate="'required|email'"
                  v-model="email"
                  name="email"
                  type="email"
                  class="form-control"
                  id="email">
              </div>
            </div>
            <div class="col-sm-6">
              <div class="form-group">
                <label for="phone">活動日期</label>
                <input type="date" class="form-control" id="phone">
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-sm-6">
              <div class="form-group">
                <label class="form__require" for="name">參加人數</label>
                <div class="row">
                  <div class="form-group d-flex col-sm-6 pl-0 pr-0">
                    <label for="adult_num" class="col-sm-4 col-form-label pr-0">
                      成人
                    </label>
                    <div class="input-group col-sm-8 pl-0 pr-0">
                      <input
                        v-validate="'required|numeric|peopleNumber'"
                        v-model="adult_num"
                        name="adult_num"
                        type="number"
                        class="form-control text-center"
                        id="adult_num">
                    </div>
                  </div>
                  <div class="form-group d-flex col-sm-6 pl-0 pr-0">
                    <label for="child_num" class="col-sm-4 col-form-label pr-0">
                      小孩
                    </label>
                    <div class="input-group col-sm-8 pl-0 pr-0">
                      <input
                        v-validate="'required|numeric|peopleNumber'"
                        v-model="child_num"
                        name="child_num"
                        type="number"
                        class="form-control text-center"
                        id="child_num">
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="col-sm-6">
              <div class="form-group">
                <label for="phone">優惠代碼</label>
                <input type="text" class="form-control" id="phone">
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-sm-12">
              <div class="form-group">
                <label for="memo">
                  備註
                </label>
                <textarea rows="6" class="form-control" id="memo"></textarea>
              </div>
            </div>
          </div>
          <div class="rule custom-control custom-checkbox mb-2">
            <input v-validate="'required'" v-model="accept" name="accept" type="checkbox" class="custom-control-input" id="acceptRule">
            <label
              class="custom-control-label"
              for="acceptRule"
            >
              我已閱讀並同意
              <span class="rule__hight-line">
                票券訂購暨使用須知
              </span>
              內容所有條款
            </label>
          </div>
          <div class="d-flex justify-content-end">
            <button type="button" class="btn btn-secondary mr-4">
              取消
            </button>
            <button type="button" class="btn btn-primary" @click="nextStep">
              下一步
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data () {
    return {
      email: '',
      name: '',
      phone: '',
      adult_num: 0,
      child_num: 0,
      accept: false,
      orderOpen: false
    }
  },
  created () {
    this.$validator.extend('peopleNumber', {
      getMessage: field => '請至少有一個人參加',
      validate: () => {
        return this.adult_num > 0 || this.child_num > 0
      }
    })
  },
  methods: {
    nextStep () {
      this.$validator.validateAll().then((result) => {
        if (result) {
        } else {
          alert('請檢查表單內容')
        }
      })
    }
  }
}
</script>

<style lang="scss">

</style>
