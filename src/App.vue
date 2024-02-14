<script setup lang="ts">
import {ref, watch} from "vue";
import Technology from "./components/technology.vue";
import Football from "./components/football.vue";
import Sport from "./components/sport.vue";
import Stadion from "./components/stadion.vue";
import Kazan from "./components/kazan.vue";

const selected = ref(0);

watch(() => selected.value, (id: typeof selected.value) => {
  switch (id) {
    case 1: {
      console.log("Нажата кнопка 1")
      break;
    }
    case 2: {
      console.log("Нажата кнопка 2")
      break;
    }
    case 3: {
      console.log("Нажата кнопка 3")
      break;
    }
    case 4: {
      console.log("Нажата кнопка 4")
      break;
    }
    case 5: {
      console.log("Нажата кнопка 5")
      break;
    }
  }
})

const onClickContainer = () => {
  selected.value = 0
}

const onClickBlock = (id: number) => {
  if (selected.value === id) {
    selected.value = 0
  } else {
    selected.value = id
  }
}
</script>

<template>
  <div class="container" @click="onClickContainer">
    <div class="title"></div>
    <div class="blocks">
      <div class="block" :class="selected == 1 ? 'selected' : ''" @click.stop="onClickBlock(1)">
        <Kazan class="bg"/>
      </div>
      <div class="block" :class="selected == 2 ? 'selected' : ''" @click.stop="onClickBlock(2)">
        <Technology class="bg"/>
      </div>
      <div class="block" :class="selected == 3 ? 'selected' : ''" @click.stop="onClickBlock(3)">
        <Football class="bg"/>
      </div>
      <div class="block" :class="selected == 4 ? 'selected' : ''" @click.stop="onClickBlock(4)">
        <Sport class="bg"/>
      </div>
      <div class="block" :class="selected == 5 ? 'selected' : ''" @click.stop="onClickBlock(5)">
        <Stadion class="bg"/>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
