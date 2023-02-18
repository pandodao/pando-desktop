<template>
  <div class="intro">
    <!-- <div class="intro-title">Service Introduction</div> -->
    <div class="item"  v-for="item in handledItems" :key="`item-${item.name}`" @click="select(item)" >
      <div class="item-conn"></div>
      <div class="item-content">
        <div class="label">{{ item.label }}</div>
        <div class="text">{{ item.text }}</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import {ref, computed} from 'vue'
import homeIcon from '../assets/images/logo.svg'
import fswapIcon from '../assets/images/products/4swap.svg'
import leafIcon from '../assets/images/products/leaf.svg'
import ringsIcon from '../assets/images/products/rings.svg'
import catkinIcon from '../assets/images/products/catkin.svg'
import bazaarIcon from '../assets/images/products/bazaar.svg'

const props = defineProps<{
  items: Array<any>
}>()

const emit = defineEmits({
  "select": (tab: any) => {}
});

const iconMap:Record<string, any> = {
  "home": homeIcon,
  "fswap": fswapIcon,
  "leaf": leafIcon,
  "rings": ringsIcon,
  "catkin": catkinIcon,
  "bazaar": bazaarIcon,
}

const handledItems = computed(() => {
  const ret = []
  for (let ix = 0; ix < props.items.length; ix++) {
    if (ix === 0) {
      continue;
    }
    const item:any = props.items[ix] as any;
    item.icon = iconMap[item.name];
    ret.push(item)
  }
  return ret;
})

function select(tab:any) {
  emit("select", tab)
}

</script>

<style lang="scss" scoped>
.intro {
  text-align: left;
  padding: 20px 0;
  .intro-title {
    margin-bottom: 20px;
    font-size: 1.1rem;
    font-weight: bold;
  }
  .item {
    padding: 8px 0 ;
    margin-bottom: 10px;
    display: flex;
    max-width: 340px;
    height: 64px;
    // background: white;
    // border-radius: 8px;
    img {
      border-radius: 99em;
      flex-basis: 32px;
    }
    .item-conn {
      width: 48px;
      height: 1px;
      background: rgba(0,0,0,0.1);
      transform: translateY(16px);
      &::after {
        width: 44px;
        height: 1px;
        background: rgba(0,0,0,0.1);
        display: block;
        content: " ";
        position: absolute;
        transform: rotate(45deg) translateX(40px) translateY(-18px);
      }
    }
    .item-content {
      border-bottom: 1px solid rgba(0,0,0,0.1);
      margin-left: 31px;
      padding-bottom: 20px;
      flex: 1;
      text-align: left;
      .text {
        font-size: 0.8rem;
        color: #666;
      }
    }
  }

}
</style>