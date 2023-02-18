<template>
  <div class="tabs">
    <div class="tab" :class="item.selected? 'selected': ''" v-for="item in handledItems" :key="item.name" @click="select(item)" >
      <img :src="item.icon" width="32" height="32"/>
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

const tabSelected = ref("home")

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
    const item:any = props.items[ix] as any;
    item.icon = iconMap[item.name];
    item.selected = tabSelected.value === item.name;
    ret.push(item)
  }
  return ret;
})

function select(tab:any) {
  tabSelected.value = tab.name
  emit("select", tab)
}

</script>

<style lang="scss" scoped>
.tabs {
  padding: 20px 8px;
  height: 100vh;
  .tab {
    margin-bottom: 10px;
    padding: 8px;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 64px;
    height: 64px;
    img {
      border-radius: 99em;
    }
  }
  .tab.selected {
    background: #ECECFA;
    border-radius: 8px;
  }
}
</style>