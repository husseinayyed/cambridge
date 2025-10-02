<script setup>
import gsap from "gsap";
import { SplitText } from "gsap/SplitText";
import { onMounted, ref } from "vue";
import { titles } from "./helpers/data";
import Card from "./components/Card.vue";
gsap.registerPlugin(SplitText);
const progress = ref(null);
const handleScroll = () => {
  const scrollPosition = window.scrollY;
  const viewHeight = document.documentElement.scrollHeight - window.innerHeight;
  const scrollProgress = (scrollPosition / viewHeight) * 100
  gsap.to(progress.value,{
    width:`${scrollProgress}%`,
    duration:0.1,
    ease:"none"
  })
};
onMounted(() => {
  window.addEventListener("scroll",handleScroll)
  document.fonts.ready.then(() => {
    const splitTitle = new SplitText("h1.title", {
      type: "words",
      wordsClass: "word",
    });
    const splitTitle2 = new SplitText(".subtitle", {
      type: "words",
      wordsClass: "word",
    });
    const tl = gsap.timeline();
    tl.from(splitTitle.words, {
      duration: 0.8,
      ease: "power2.out",
      y: 50,
      opacity: 0,
      stagger: 0.3,
    });
    tl.from(
      splitTitle2.words,
      {
        duration: 0.6,
        ease: "power2.out",
        y: 30,
        opacity: 0,
        stagger: 0.2,
      },
      "+=0.2"
    );
  });
});
</script>

<template>
  <div class="progress" ref="progress"></div>
  <main>
    <h1 class="title gold">{{ titles.title }}</h1>
    <p class="subtitle bold">{{ titles.subtitle }}</p>
  </main>
  <Card />
</template>

<style scoped>
main {
  display: flex;
  flex-flow: column wrap;
  width: 100%;
  height: 100vh;
  align-items: center;
  justify-content: center;
}
.progress {
  position: fixed;
  top: 0;
  left: 0;
  width: 0;
  height: 4px;
  border-radius: 4px;
  background-color: #ffd720;
  z-index: 10;
}
</style>
