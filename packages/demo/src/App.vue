<template>
  <VueWinBox
    ref="winboxRef"
    :options="options"
    @onfocus="isOpen = true"
    @onclose="isOpen = false"
  >
    <Counter @update:count="setTitle" />
  </VueWinBox>
  <div class="container">
    <div class="button" v-show="!isOpen" @click="initialize">Open Vue component</div>
    <div class="button" @click="openUrl" style="margin-top: 10px;">Open Random URL</div>
  </div>
</template>

<script lang="ts">
import { defineComponent, onMounted, onUnmounted, ref } from 'vue'
import VueWinBox, { useWinBox } from 'vue-winbox'
import Counter from './Counter.vue'

export default defineComponent({
  components: {
    VueWinBox,
    Counter
  },
  setup() {
    const options = {
      title: 'Count: 0',
      class: 'modern',
      x: 'center',
      y: 'center',
      width: '50%',
      height: '50%'
    }
    const winboxRef = ref()
    const isOpen = ref(true)
    const createWinBox = useWinBox()

    const setTitle = (count: number) => {
      winboxRef.value?.winbox?.setTitle('Count: ' + count)
    }

    // TODO: Check winbox status before resizing
    // const handleResize = () => {
    //   winboxRef.value?.winbox?.resize("50%", "50%").move("center", "center")
    // }

    // onMounted(() => {
    //   window.addEventListener('resize', handleResize)
    // })

    // onUnmounted(() => {
    //   window.removeEventListener('resize', handleResize)
    // })

    const initialize = () => {
      winboxRef.value?.initialize()
    }
    
    const openUrl = () => {
      const randomId = Math.floor(Math.random() * 20) + 1
      createWinBox({
        title: `Fox #${randomId}`,
        url: `https://randomfox.ca/images/${randomId}.jpg`,
        class: 'modern'
      })
    }

    return {
      options,
      winboxRef,
      setTitle,
      initialize,
      isOpen,
      openUrl
    }
  }
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
}

html, body {
  height: 100vh;
  font-family: -apple-system, BlinkMacSystemFont, Helvetica, Arial, "Open Sans", OpenSans, Roboto, Segoe UI, sans-serif;
  background: linear-gradient(135deg, #0d1117, #131820);
}

.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.button {
  padding: 5px 10px;
  margin-bottom: 5px;
  display: inline-block;
  background-color: #ca00b4;
  color: #fff;
  width: auto;
  border-radius: 10px;
  padding: 15px 25px;
  cursor: pointer;
}
</style>