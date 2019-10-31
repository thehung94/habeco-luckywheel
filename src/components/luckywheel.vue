<template>
    <div class="container">
        <div class="lucky-wheel">
            <div class="wheel-main">
                <div class="wheel-pointer-box">
                     <div class="wheel-pointer" @click="rotate_handle()" :style="{transform:rotate_angle_pointer,transition:rotate_transition_pointer}"></div>
                </div>               
                <div class="wheel-bg" :style="{transform:rotate_angle,transition:rotate_transition}">                   
                    <div class="prize-list">
                        <div class="prize-item" v-for="(item,index) in prize_list" :key="index">
                            <div class="prize-pic">
                                <img :src="item.icon" v-show="item.icon != '#'" :style="item.style">
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
export default {
  data() {
    return {
      easejoy_bean: 0,
      lottery_ticket: 0,
      prize_list: [
        {
          icon: require("../assets/img/habeco/prize_1.png")
        },
        {
          icon: "#"
        },
        {
          icon: require("../assets/img/habeco/prize_3.png")
        },
        {
          icon: require("../assets/img/habeco/prize_4.png")
        },
        {
          icon: require("../assets/img/habeco/prize_5.png"),
          style: "width: 1.7rem" 
        },
        {
          icon: require("../assets/img/habeco/prize_6.png")
        },
        {
          icon: require("../assets/img/habeco/prize_7.png")
        },
        {
          icon: require("../assets/img/habeco/prize_2.png")
        }
      ],
      toast_control: false,
      hasPrize: false,
      start_rotating_degree: 0,
      rotate_angle: 0,
      start_rotating_degree_pointer: 0,
      rotate_angle_pointer: 25,
      rotate_transition: "transform 6s ease-in-out",
      rotate_transition_pointer: "transform 12s ease-in-out",
      click_flag: true,
      index:  0
    };
  },
  created() {
    this.init_prize_list();
  },
  computed: {
    
  },
  methods: {
    init_prize_list(list) {},
    rotate_handle() {
      this.index = 0;
      this.rotating();
    },
    rotating() {
      if (!this.click_flag) return;
      var type = 0;
      var during_time = 0;
      var random = Math.floor(Math.random() * 7);
      var result_index = random ;
      var result_angle = [337.5, 292.5, 247.5, 202.5, 157.5, 112.5, 67.5, 22.5];
      var rand_circle = 6;
      this.click_flag = false;
      if (type == 0) {
        // 转动盘子
        var rotate_angle =
          this.start_rotating_degree +
          rand_circle * 360 +
          result_angle[result_index] -
          this.start_rotating_degree % 360;
        this.start_rotating_degree = rotate_angle;
        this.rotate_angle = "rotate(" + rotate_angle + "deg)";
        
        var that = this;

        setTimeout(function() {
          that.click_flag = true;
          that.game_over();
        }, 20000);
      } else {
        //
      }
    },
    game_over() {
      this.toast_control = false;
      this.hasPrize = this.prize_list[this.index].isPrize
    },
    //关闭弹窗
    close_toast() {
      this.toast_control = false;
    }
  }
};
</script>
<style scoped>
.container {
  width: 100%;
}
.lucky-wheel {
  width: 100%;
  height: 19rem;
  background-size: 100%;
}
.wheel-main {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  padding-top: 1rem;
}
.wheel-bg {
  width: 15rem;
  height: 15rem;
  background: url("../assets/img/habeco/wheel_list.png") no-repeat center top;
  background-size: 100%;
  color: #fff;
  font-weight: 500;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  transition: transform 3s ease;
}
.wheel-pointer-box {
  position: absolute;
  top: 59%;
  left: 50%;
  z-index: 100;
  transform: translate(-50%, -60%);
  width: 5rem;
  height: 7.8rem;
}
.wheel-pointer {
  width: 5rem;
  height: 7.8rem;
  background: url("../assets/img/habeco/pointer.png") no-repeat center top;
  background-size: 100%;
  transform-origin: center 60%;
}
.wheel-bg div {
  text-align: center;
}
.prize-list {
  width: 100%;
  height: 100%;
  position: relative;
}
.prize-list .prize-item {
  position: absolute;
  top: 0;
  left: 0;
  z-index: 2;
}
.prize-list .prize-item:first-child {
  top: 0;
  left: 6rem;
  transform: rotate(24deg);
}
.prize-list .prize-item:nth-child(2) {
  top: 2.8rem;
  left: 10.8rem;
  transform: rotate(67deg);
}
.prize-list .prize-item:nth-child(3) {
  top: 4.3rem;
  left: 7.6rem;
  transform: rotate(-250deg);
}
.prize-list .prize-item:nth-child(4) {
  top: 5.9rem;
  left: 5.8rem;
  transform: rotate(-206deg);
}
.prize-list .prize-item:nth-child(5) {
  top: 6.2125rem;
  left: 3.4rem;
  transform: rotate(-160deg);
}
.prize-list .prize-item:nth-child(6) {
  top: 4.35rem;
  left: 1.5rem;
  transform: rotate(-111deg);
}
.prize-list .prize-item:nth-child(7) {
  top: 1.8rem;
  left: 1.8rem;
  transform: rotate(-69deg);
}
.prize-list .prize-item:nth-child(8) {
  top: 0;
  left: 3.5rem;
  transform: rotate(-20deg);
}
.prize-item {
  width: 5.875rem;
  height: 9rem;
}

.prize-pic img {
  width: 1rem;
  height: 3rem;
  margin-top: 1.5625rem;
}
.prize-count {
  font-size: 0.875rem;
}
.prize-type {
  font-size: 0.75rem;
}
.main {
  position: relative;
  width: 100%;
  min-height: 14.25rem;
  background: rgb(243, 109, 86);
  padding-bottom: 1.6875rem;
}
.main-bg {
  width: 100%;
  height: 6.5625rem;
  position: absolute;
  top: -3.4375rem;
  left: 0;
  background: url("../assets/img/luck_bg.png") no-repeat center top;
  background-size: 100%;
}
.bg-p {
  width: 100%;
  height: 2.95rem;
  background: rgb(252, 207, 133);
}
.content {
  position: absolute;
  top: 0.175rem;
  left: 0;
  background: rgb(243, 109, 86);
  width: 100%;
  height: 5.1875rem;
  font-size: 1.125rem;
  color: #ffeb39;
  padding-left: 6.75rem;
}
.content div {
  text-align: left;
}
.tip {
  position: relative;
  margin: 2.5rem auto 0;
  width: 17.5rem;
  border: 1px solid #fbc27f;
}
.tip-title {
  position: absolute;
  top: -1rem;
  left: 50%;
  transform: translate(-50%, 0);
  font-size: 1rem;
  color: #fccc6e;
  background: rgb(243, 109, 86);
  padding: 0.3125rem 0.625rem;
}
.tip-content {
  padding: 1.5625rem 0.625rem;
  font-size: 0.875rem;
  color: #fff8c5;
  line-height: 1.5;
}
.toast-mask {
  position: fixed;
  top: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.6);
  z-index: 10000;
  width: 100%;
  height: 100%;
}
.toast {
  position: fixed;
  top: 50%;
  left: 50%;
  z-index: 20000;
  transform: translate(-50%, -50%);
  width: 15.4375rem;
  background: #fff;
  border-radius: 0.3125rem;
  padding: 0.3125rem;
  background-color: rgb(252, 244, 224);
}
.toast-container {
  position: relative;
  width: 100%;
  height: 100%;
  border: 1px dotted #fccc6e;
}
.toast-picture {
  position: absolute;
  top: -6.5rem;
  left: -1.5rem;
  width: 18.75rem;
  height: 8.5625rem;
}
.toast-pictrue-change {
  position: absolute;
  top: -1.5rem;
  left: -1.375rem;
  width: 17.5rem;
  height: 3.125rem;
}
.toast-title {
  padding: 2.8125rem 0;
  font-size: 18px;
  color: #fc7939;
  text-align: center;
}
.toast-btn {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 0.9375rem;
}
.toast-btn div {
  background-image: -moz-linear-gradient(
    -18deg,
    rgb(242, 148, 85) 0%,
    rgb(252, 124, 88) 51%,
    rgb(252, 124, 88) 99%
  );

  background-image: -ms-linear-gradient(
    -18deg,
    rgb(242, 148, 85) 0%,
    rgb(252, 124, 88) 51%,
    rgb(252, 124, 88) 99%
  );
  background-image: -webkit-linear-gradient(
    -18deg,
    rgb(242, 148, 85) 0%,
    rgb(252, 124, 88) 51%,
    rgb(252, 124, 88) 99%
  );
  box-shadow: 0px 4px 0px 0px rgba(174, 34, 5, 0.7);
  width: 4.6875rem;
  height: 1.875rem;
  border-radius: 1.875rem;
  text-align: center;
  line-height: 1.875rem;
  color: #fff;
}
.close {
  position: absolute;
  top: -0.9375rem;
  right: -0.9375rem;
  width: 2rem;
  height: 2rem;
  background: url("../assets/img/close_store.png") no-repeat center top;
  background-size: 100%;
}
</style>

