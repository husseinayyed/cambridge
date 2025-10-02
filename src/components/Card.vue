<script setup>
import gsap from "gsap";
import { onMounted } from "vue";
import { SplitText } from "gsap/SplitText";
import { ScrollTrigger } from "gsap/ScrollTrigger";
import { msgs } from "../helpers/data";
gsap.registerPlugin(ScrollTrigger, SplitText);

onMounted(() => {
  document.fonts.ready.then(() => {
    const cards = gsap.utils.toArray(".card-wrapper");

    const devSplit = new SplitText("footer h2", { type: "chars" });
    cards.forEach((cardWrapper, index) => {
      gsap.context(() => {
        const nameSplit = new SplitText(".name", { type: "words" });
        const tl1 = gsap.timeline({
          scrollTrigger: {
            trigger: cardWrapper,
            start: "top 60%",
            end: "bottom 10%",
            toggleActions: "play none none reverse",
          },
        });
        if (index == 0) {
          tl1.from(".card", {
            duration: 0.8,
            width: "0px",
            opacity: 0,
            x: -10,
            ease: "power1.inOut",
          });
        }
        tl1.from(
          nameSplit.words,
          {
            duration: 0.6,
            y: 30,
            opacity: 0,
            ease: "power2.out",
            stagger: 0.3,
          },
          "-=0.2"
        );

        tl1.from(
          ".card",
          {
            duration: 0.4,
            height: "70px",
            ease: "power1.inOut",
          },
          "+=0.1"
        );

        tl1.from(
          ".content",
          {
            duration: 0.4,
            opacity: 0,
            x: -1,
            y: -2,
            ease: "power1.inOut",
          },
          "+=0.3"
        );
         tl1.from(
          ".line",
          {
            duration: 0.4,
            opacity: 0,
            ease: "power1.inOut",
          },
          "+=0.3"
        );
      }, cardWrapper); // Scope to the card wrapper
    });
    gsap.from(devSplit.chars,{
      y:10,
      opacity:0,
      duration:0.8,
      stagger:0.05,
      scrollTrigger:{
        trigger:"footer h2",
        start:"bottom 90%",
        end:"bottom bottom",
        toggleActions: "play none none reverse"
      }
    })
  });
});
</script>
<template>
  <div class="card-wrapper" v-for="(p, index) in msgs">
    <div class="card">
      <div class="header context">
        <h2
          class="name"
        >
          {{ p.name }}
        </h2>
      </div>
      <div class="content context">
        <p class="dec">
          {{ p.msg }}
        </p>
      </div>
    </div>
    <div class="line"></div>
  </div>
  <footer>
    <h2 class="footer">Devolped By Hussein Ayed</h2>
  </footer>
</template>
<style scoped>
.card-wrapper {
  width: 100%;
  display: flex;
  justify-content: center;
  flex-flow: column wrap;
}
.card {
  width: 100%;
  background-color: #111;
  padding: 0 10px;
  overflow: hidden;
  border: 1.5px solid #FFD720 ;
  border-radius: 15px;
  position: relative;
}

.line {
  position: relative;
  left: 50%;
  transform: translateX(-50%);
  width: 2px;
  border-radius: 4px;
  background-color: var(--text-title);
  height: 450px;
}
footer h2 {
  text-align: center;
}
</style>
