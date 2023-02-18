
<template>
  <!-- <img id="logo" alt="Wails logo" src="./assets/images/logo-universal.png"/> -->
  <!-- <HelloWorld/> -->
  <div class="container">
    <Tabs :items="items" @select="selectTab" />
    <div class="frames" ref="frames">
      <div class="frame home" data="home">
        <div class="logo-wrapper">
          <img src="./assets/images/logo-with-text.svg" />
        </div>
        <Home :items="items" @select="selectItem" />
      </div>
    </div>
    <div class="chat">

    </div>
  </div>
</template>

<script lang="ts" setup>
import {onMounted, Ref, ref} from 'vue'

import Tabs from './components/Tabs.vue'
import Home from './components/Home.vue'

const frames = ref(null);

const items:Ref<any> = ref([{
  name: "home",
  label: "Pando Proto",
  text: "Home",
  url: "https://pando.proto"
}, {
  name: "fswap",
  label: "4swap",
  text: "The decentralized exchange protocol",
  url: "https://app.4swap.org"
}, {
  name: "leaf",
  label: "Pando Leaf",
  text: "Mint pUSD",
  url: "https://leaf.pando.im"
}, {
  name: "rings",
  label: "Pando Rings",
  text: "The decentralized lending protocol",
  url: "https://rings.pando.im"
}, {
  name: "catkin",
  label: "Pando Catkin",
  text: "Get free cryptos and token faucets",
  url: "https://catkin.pando.im"
}, {
  name: "bazaar",
  label: "Bazaar",
  text: "A online shopping mall for digital goods",
  url: "https://bazaar.mixin.fan"
}]);

function selectTab(tab:any) {
  if (frames != null && frames.value != null) {
    const c:any = frames.value
    const existing = c.querySelector(".frame." + tab.name)
    if (existing) {
      existing.style.display = "block";
    } else {
      const frame = document.createElement("iframe");
      frame.className = "frame " + tab.name;
      frame.setAttribute("data", tab.name);
      frame.src = tab.url;
      c.appendChild(frame);
    }
    const allFrames = c.querySelectorAll(".frame")
    for (let ix = 0; ix < allFrames.length; ix++) {
      const element = allFrames[ix];
      console.log(element)
      if (element.getAttribute("data") !== tab.name) {
        element.style.display = "none";
      } else {
        element.style.display = "block";
      }
    }
  }
}

function selectItem(item:any) {
  selectTab(item)
}

onMounted(() => {
  const frames = ("frames");
  console.log(frames);
  setTimeout(()=> {
    selectTab(items.value[0])
  }, 1000)
})

</script>

<style>
* {
  box-sizing: border-box;
}

.container {
  display: flex;
  flex-direction: row;
  height: 100%;
  width: 100%;
  background-color: #F8FAFB;
}
</style>
<style lang="scss" scoped>
.frames {
  height: 100vh;
  flex: 1;
  &:deep(.frame) {
    width: 100%;
    height: 100%;
    border: none;
  }
}
.logo-wrapper {
  max-height: 32px;
  margin: 34px 0 16px 0;
  img {
    height: 32px;
    width: 100%;
  }
}
.chat {
  flex-basis: 300px;
  display: none;
}
</style>
