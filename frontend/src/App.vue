<template>
  <div>
    <div class="info">스크롤을 내리면 책상이 보입니다.</div>
    <div class="contents">
      <img src="./assets/imgs/desk.jpg" class="initDesk bgDesk" alt="bgDesk" />
      <img src="./assets/imgs/frame.png" class="addItem frame" alt="frame" />
      <img src="./assets/imgs/soap.png" class="addItem soap" alt="soap" />
      <img src="./assets/imgs/card.png" class="addItem card" alt="card" />
      <img src="./assets/imgs/postit.png" class="addItem postit" alt="postit" />
      <img src="./assets/imgs/wallet.png" class="addItem wallet" alt="wallet" />
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
gsap.defaults({ ease: "Power1.easeInOut", duration: 2 });

export default defineComponent({
  name: "bgDesk",
  mounted() {
    this.deskPin();
  },
  methods: {
    deskPin() {
      const tl = gsap.timeline();
      tl.from(".frame", { yPrecent: -100, opacity: 1 });

      ScrollTrigger.create({
        animation: tl,
        trigger: ".bgDesk",
        start: "center center",
        end: "+=4000",
        markers: true,
        pin: true,
        toggleActions: "restart pause pause reverse",
      });

      /* gsap.to(".bgDesk", {
        scrollTrigger: {
          trigger: ".bgDesk",
          start: "center center",
          end: "+=4000",
          markers: true,
          pin: true,
          toggleActions: "restart pause pause reverse",
        },
        display: "block",
        opacity: 1,
      }); */
    },
  },
});
</script>

<style scoped>
.info {
  width: 90vw;
  height: 80vh;
  padding: 250px 0 50px 0;
  font-size: x-large;
}
.contents {
  position: relative;
  width: 480px;
  height: 800px;
}
.bgDesk {
  opacity: 1;
  width: 400px;
  height: 600px;
  margin: 0 auto 100px auto;
  position: absolute;
  top: 0;
  left: 450px;
}
.addItem {
  margin: 0 auto;
  position: absolute;
  top: 0;
  left: 450px;
  opacity: 0;
}
.frame {
  width: 400px;
  height: 600px;
}
.postit {
  width: 400px;
  height: 600px;
}
.card {
  width: 400px;
  height: 600px;
}
.soap {
  width: 400px;
  height: 600px;
}
.wallet {
  width: 400px;
  height: 600px;
}
</style>
