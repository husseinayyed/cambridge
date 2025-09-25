<script setup>
import gsap from "gsap";
import { SplitText } from "gsap/SplitText";
import { onMounted } from "vue";
import { msgs, titles } from "./helpers/data";
import Card from "./components/Card.vue";
gsap.registerPlugin(SplitText);
onMounted(() => {
  document.fonts.ready.then(() => {
    const splitTitle = new SplitText("h1.title", {
      type: "words",
      wordsClass: "word"
    });
    const splitTitle2 = new SplitText(".subtitle", {
      type: "words",
      wordsClass: "word"
    });
    const tl = gsap.timeline()
    tl.from(splitTitle.words, {
      duration: 0.8,
      ease: "power2.out",
      y: 50,
      opacity: 0,
      stagger: 0.3
    });
    tl.from(splitTitle2.words, {
      duration: 0.6,
      ease: "power2.out",
      y: 30,
      opacity: 0,
      stagger: 0.2
    },"+=0.2");

  });
  
});

</script>

<template>
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
</style>
