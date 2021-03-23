<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'HelloWorld',
  props: {
    msg: String
  },
  setup () {
    const num = ref<number>(111);
    const sayHi = (source: string): void => {
      console.log(`Hi —— from ${source}.`);
    }

    // 父组件的模板可以响应更新
    setTimeout(() => {
      num.value = 333;
    }, 2000);

    return {
      // 数据不 return 的话，方式一会拿不到
      num,

      // 方法需要 return 出去，才能执行
      sayHi
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
