<template>
  
  <fieldset>
    <legend>Заявка</legend>
    <div>
      <div><label>Ваше имя: <input type="text" name="token" v-model="name" placeholder="Введите Ваше имя"
            required></label></div>
      <div><label>Ваш номер телефона: <input type="phone" name="token" v-model="phone"
            placeholder="Введите Ваш номер телефона" required></label>
        <div><label>Ваше сообщение: <textarea name="token" v-model="message" placeholder="Введите Ваше сообщение" id=""
              cols="30" rows="10" wrap="soft" required></textarea></label></div>
      </div>
    </div>
    <div>
      <button @click.prevent="subm()">отправить</button>
    </div>
  </fieldset>
  
</template>

<script setup>
import { ref } from 'vue';

let name = ref('');
let phone = ref('');
let message = ref('');

const subm = () => {
  // Проверка на заполненность полей
  if (!name.value || !phone.value || !message.value) {
    console.error('Все поля должны быть заполнены.');
    return; // Не отправляем запрос, если поля пустые
  }

  const data = {
    name: name.value,
    phone: phone.value,
    message: message.value,
  };
    console.log(data);
  const jsonData = JSON.stringify(data);

    // Отправляем POST-запрос на сервер
  fetch('http://127.0.0.1:8000/applications/create/', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',  // Указываем, что отправляем JSON
      },
      body: jsonData,  // Преобразуем объект в JSON
  }).then(res => {
    if (!res.ok) {
        return Promise.reject()
    }
    return res;
  }).then(res => console.log("All cool!"))
  .catch(err => {console.log("Error!");console.log(err);});
    // Обработать ошибку (например, проблемы с сетью)
};
</script>

<style>
.TextArea {
  width: 100%;
}
</style>

