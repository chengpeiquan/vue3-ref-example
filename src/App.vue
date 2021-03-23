<template>
  <img
    ref="logo"
    class="logo"
    alt="Vue logo"
    src="./assets/logo.png"
  >

  <p v-if="child">{{ child.num }}</p>

  <div>
    <button @click="child.sayHi('template')">Say Hi</button>
  </div>

  <Child
    ref="child"
    msg="Welcome to Your Vue.js + TypeScript App"
  />
</template>

<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';
import Child from './components/Child.vue';

export default defineComponent({
  name: 'App',
  components: {
    Child
  },
  setup () {
    // DOM
    const logo = ref<HTMLImageElement | null>(null);

    // 子组件，使用 typeof 获取子组件的类型
    const child = ref<typeof Child | null>(null);

    onMounted( () => {
      /** 
       * 可选方式一：通过 TS 的可选符 ? 来将目标设置为可选，避免出现错误
       * 这个方式不能修改子组件的值
       */
      console.log(logo.value?.getAttribute('src'));
      console.log(child.value?.num);
      child.value?.sayHi('use ? in onMounted');

      console.log('------------------------------');
      

      /** 
       * 可选方式二：判断 value 存在时再执行操作
       * 这个方式可以正常修改子组件的值
       */

      if ( logo.value ) {
        console.log(logo.value.getAttribute('src'));
      }

      if ( child.value ) {
        child.value.num = 222;
        console.log(child.value.num);
        child.value.sayHi('use if in onMounted');
      }
    })

    return {
      logo,
      child
    }
    
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
