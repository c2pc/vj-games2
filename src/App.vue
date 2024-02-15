<script setup lang="ts">
import {ref, watch} from "vue";
import Technology from "./components/technology.vue";
import Football from "./components/football.vue";
import Sport from "./components/sport.vue";
import Stadion from "./components/stadion.vue";
import Kazan from "./components/kazan.vue";
import axios from "axios"; // Импорт Axios


// Функция для отправки OSC сообщений теперь принимает адрес OSC в качестве параметра
const sendOscMessage = (address, id) => {
  axios.post('http://10.30.38.118:3000/send-osc', {
    address, // Используйте переданный адрес
    args: [id],
  })
      .then(() => console.log(`OSC message sent for address: ${address} with id: ${id}`))
      .catch(error => console.error('Error sending OSC message:', error));
};



const selected = ref(0);

watch(() => selected.value, (newVal, oldVal) => {
  if (newVal === 0 && oldVal !== 0) {
    // Здесь отправляем OSC сообщение при отжатии кнопки
    sendOscMessage('/composition/columns/1/connect', oldVal); // Используйте соответствующий адрес и предыдущее значение id как аргумент
    console.log(`Кнопка ${oldVal} отжата`);
  } else if (newVal !== 0) {
    // Остальная логика для нажатия кнопок
    console.log(`Нажата кнопка ${newVal}`);
    switch (newVal) {
      case 1:
        sendOscMessage('/composition/columns/10/connect', 1);
        break;
      case 2:
        sendOscMessage('/composition/columns/8/connect', 1);
        break;
      case 3:
        sendOscMessage('/composition/columns/7/connect', 1);
        break;
      case 4:
        sendOscMessage('/composition/columns/9/connect', 1);
        break;
    }
  }
});

const onClickContainer = () => {
  selected.value = 0
  sendOscMessage('/composition/columns/1/connect', 1);
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
