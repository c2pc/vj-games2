<script setup lang="ts">
import {ref, watch} from "vue";
import axios from "axios";
import Big from "./components/big.vue";
import Small from "./components/small.vue"; // Импорт Axios


// Функция для отправки OSC сообщений теперь принимает адрес OSC в качестве параметра
const sendOscMessage = (address:string, id:number) => {
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
        sendOscMessage('/composition/columns/12/connect', 1);
        break;
      case 2:
        sendOscMessage('/composition/columns/13/connect', 1);
        break;
      case 3:
        sendOscMessage('/composition/columns/10/connect', 1);
        break;
      case 4:
        sendOscMessage('/composition/columns/11/connect', 1);
        break;
      case 5:
        sendOscMessage('/composition/columns/14/connect', 1);
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
  <div @click="onClickContainer">
    <div class="container">
      <div class="title">
        <span>Выбери контент</span>
        <span>Select content</span>
      </div>
      <div class="blocks">
        <div class="block" :class="selected == 1 ? 'selected' : ''" @click.stop="onClickBlock(1)">
          <div class="text">
            <span>Казань - город Игр Будущего</span>
            <span>Kazan - games of the future city</span>
          </div>
          <Big class="bg"/>
        </div>
        <div class="block" :class="selected == 2 ? 'selected' : ''" @click.stop="onClickBlock(2)">
          <div class="text">
            <span>Технологии будущего</span>
            <span>Technologies of the future</span>
          </div>
          <Small class="bg"/>
        </div>
        <div class="block" :class="selected == 3 ? 'selected' : ''" @click.stop="onClickBlock(3)">
          <div class="text">
            <span>Фиджитал-футбол</span>
            <span>Phygital-football</span>
          </div>
          <Small class="bg"/>
        </div>
        <div class="block" :class="selected == 4 ? 'selected' : ''" @click.stop="onClickBlock(4)">
          <div class="text">
            <span>Фиджитал-спорт</span>
            <span>Phygital-sport</span>
          </div>
          <Small class="bg"/>
        </div>
        <div class="block" :class="selected == 5 ? 'selected' : ''" @click.stop="onClickBlock(5)">
          <div class="text">
            <span>Стадион будущего</span>
            <span>StadiUm of the future</span>
          </div>
          <Small class="bg"/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>
