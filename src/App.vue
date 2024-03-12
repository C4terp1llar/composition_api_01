<template>
  <div class="container">
    <div class="card">
      <h1>Vue Composition Api</h1>
      <small>data, methods, computed, watch</small>

      <div class="form-control">
        <label for="reff">ref</label>
        <input type="text" id="reff" ref="textInp">
        <label for="name">Модель name</label>
        <input type="text" id="name" v-model="fName">
      </div>

      <button class="btn" @click="change">Изменить</button>
    </div>
    <app-info
      :name="name"
      :version="version"
      @change-to-ver3="changeVer"
      class="test-from-app"
    >
     <template>footer</template>
    </app-info>
  </div>
</template>

<script>
import {ref, reactive, computed, watch, toRefs, isRef, isReactive} from 'vue';
import appInfo from "@/components/AppInfo.vue";

// для проверки isRef, isReactive
// вернет булевое значение
// console.log(isRef(name)); || console.log(isReactive(name));

/*
  reactive
  добавляет реактивность объекту (в случае работы с объектами)
  в отличии от ref (который ссылается на refImpl в котором лежит прокси обджект)
  reactive ссылается сразу на прокси обджект
*/


export default {
  setup(){
    const name = ref('VueJS');
    let version = ref(3);
    const textInp = ref(null);
    const fName = ref(null);

    const doubleVersion = computed(() => {
      return version.value * 2
    })

    // watch([doubleVersion, name], (newVals, oldVals) => {
    //   console.log(`new doubleVersion: ${newVals[0]} old doubleVersion: ${oldVals[0]}`);
    //   console.log(`new name: ${newVals[1]} old name: ${oldVals[1]}`);
    // })

    // const framework = reactive({
    //   name: 'VueJS',
    //   version: 3
    // })
  

    function changeInfo(){
      name.value = 'Vue JS!';
      version.value = 4;

      // console.log('реф на инпут: ', textInp.value);
      // console.log('реф на значение инпута: ', textInp.value.value);
      //
      // console.log('модель: ', fName);

      // framework.name = 'Vue JS!';
      // framework.version = 4;
    }

    function changeVer (val) {
      version.value = val;
    }

    return{
      // С использованием ref (отдельно созданные данные)
      name: name,
      version: version,
      doubleVersion: doubleVersion,
      // textInp: textInp,
      fName: fName,

      // С использованием ref, объект с данными
      // name: framework.value.name,
      // version: framework.value.version,
      // framework: framework,

      // C использвоанием reactive (объект с данными)
      // name: framework.name,
      // version: framework.version,

      // ...toRefs(framework),
      // // или
      // framework: framework,

      change: changeInfo,
      changeVer
    }
  },
  components: {
    appInfo,
  }
}
</script>