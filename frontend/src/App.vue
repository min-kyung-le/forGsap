<template>
  <div>
    <h1 class="top-comment">
      Scroll Down!
      <p>
        <img class="icon-down" src="./assets/chevron-down.svg" width="30" />
      </p>
    </h1>

    <section class="comparisonSection">
      <div class="comparisonImage beforeImage">
        <img src="./assets/imgs/desk.jpg" alt="desk" />
      </div>
      <div class="comparisonImage afterImage afterImage0">
        <img src="./assets/imgs/frame.png" alt="frame" />
      </div>
      <div class="comparisonImage afterImage afterImage1">
        <img src="./assets/imgs/soap.png" alt="soap" />
      </div>
      <div class="comparisonImage afterImage afterImage2">
        <img src="./assets/imgs/card.png" alt="card" />
      </div>
      <div class="comparisonImage afterImage afterImage3">
        <img src="./assets/imgs/postit.png" alt="postit" />
      </div>
      <div class="comparisonImage afterImage afterImage4">
        <img src="./assets/imgs/wallet.png" alt="wallet" />
      </div>
    </section>
    <h1 class="bottom-comment">What do you think?</h1>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import { gsap } from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

gsap.registerPlugin(ScrollTrigger);
export default defineComponent({
  name: "bgDesk",
  mounted() {
    this.sectionSlide();
    this.textAnimation();
  },
  methods: {
    textAnimation() {
      gsap.from(".icon-down", {
        duration: 0.2,
        y: 8,
        repeat: 100,
        yoyo: true,
      });

      gsap.from(".bottom-comment", {
        scrollTrigger: {
          trigger: ".bottom-comment",
          toggleActions: "restart pause restart pause",
        },
        scale: 0.3,
        stagger: 0.3,
        ease: "elastic",
        opacity: 0,
        duration: 1.5,
        force3D: true,
      });
    },
    sectionSlide() {
      gsap.utils.toArray(".comparisonSection").forEach((section) => {
        let tl = gsap.timeline({
          scrollTrigger: {
            trigger: section,
            start: "center-=100 center",
            end: () => "+=" + section.offsetWidth,
            scrub: true,
            pin: true,
            anticipatePin: 1,
          },
          defaults: { ease: "none" },
        });

        for (let i = 0; i < 5; i++) {
          tl.fromTo(
            section.querySelector(`.afterImage${i}`),
            { xPercent: 100, x: 0 },
            { xPercent: 0 }
          ).fromTo(
            section.querySelector(`.afterImage${i} img`),
            { xPercent: -100, x: 0 },
            { xPercent: 0 },
            "<"
          );
        }
      });
    },
  },
});
</script>

<style scoped>
.top-comment {
  text-align: center;
  height: 100vh;
  padding-top: 280px;
}

.top-comment p {
  margin: 7px 0 0 0;
}

.bottom-comment {
  text-align: center;
  height: 400px;
  padding-top: 300px;
}

body {
  height: 300vh;
  background-color: #111;
  color: white;
  overflow-x: hidden;
}

h1,
h2 {
  font-weight: 400;
  max-width: none;
}

.comparisonSection {
  padding-top: 150px;
  margin-left: 500px;
  position: relative;
  padding-bottom: 56.25%; /* to maintain aspect ratio (responsive!) */
}
.comparisonImage {
  width: 30%;
  height: 80%;
}

.comparisonImage img {
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
}
.afterImage {
  position: absolute;
  overflow: hidden;
  top: 0;
  transform: translate(100%, 0px);
}

.beforeImage img {
  width: 30%;
  height: 80%;
}
</style>
