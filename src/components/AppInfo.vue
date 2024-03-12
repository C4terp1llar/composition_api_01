<template>
  <div class="card">
    <p>Название: <strong>{{name}}</strong></p>
    <p>Версия: {{version}} ({{doubleVersion}})<strong></strong></p>

    <button class="btn warning" @click="changeVersion">На 3 версию</button>
  </div>
</template>

<script >
import {computed} from 'vue'

/*

для реботы с пропсами в композишн апи, нужно передавать их в параметре сетапу
для ряботы с эмитами, слотами и атрсами используется context, который тоже передается в параметрах сетапу

*/
export default {
  props: ['name', 'version'],
  emits: ['changeToVer3'],
  setup(props, context){
    const doubleVersion = computed(() => {
      return props.version * 2;
    })

    function change(){
      context.emit('changeToVer3', 3);
      console.log(context)
    }

    return{
      doubleVersion,
      changeVersion: change
    }
  }
}
</script>

<style scoped>

</style>