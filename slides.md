---
theme: seriph
background: https://cover.sli.dev
title: FSM и диалоги в Aiogram
class: text-center
highlighter: shiki
transition: slide-left
# mdc: true
---

# Диалоги в Aiogram и FSM

---
layout: center
---

<h3>Как на сайтах пользователи заполняют данные</h3>

<v-click>
<div class="w-full mt-3">
    <form class="w-full flex flex-col gap-3">
        <input class="w-1/2 border border-gray-500 rounded px-2" type="text" placeholder="Ваше имя" /> 
        <input class="w-1/2 border border-gray-500 rounded px-2" type="number" placeholder="Ваш возраст" min="10" max="100"/>
        <label class="w-full">
            Ваш пол:
            <select class="px-2">
                <option>Мужской</option>
                <option>Женской</option>
            </select>
        </label>
        <label class="w-full">
            Ваш любимый жанр книг:
            <select class="px-2">
                <option>Фантастика</option>
                <option>Детектив</option>
                <option>Роман</option>
                <option>Приключения</option>
            </select>
        </label>
        <input class="w-full border border-gray-500 rounded px-2" type="text" value="" placeholder="Ваша любимая книга" />
    </form>
</div>
</v-click>

---
layout: center
---

<h3> Как на сайтах пользователи заполняют данные </h3>
<v-click>
<div class="w-full mt-3">
    <form class="w-full flex flex-col gap-3">
        <h4>Оставьте отзыв о нашем сервисе</h4>
        <input class="w-1/2 border border-gray-500 rounded px-2" type="text" placeholder="Ваше имя" />
        <input class="w-1/2 border border-gray-500 rounded px-2" type="text" placeholder="Ваш номер телефона" />
        <div class="w-2/3 flex flex-wrap gap-3">
            <label class="w-full">Понравилось ли Вам наше обслуживание?</label>
            <button type="button">Да</button><button type="button">Нет</button>
        </div>
        <textarea class="w-full border border-gray-500 rounded px-2" value="" placeholder="Оставьте свои пожелания">
        </textarea>
    </form>
</div>
</v-click>

<style>
    button {
        border: 1px solid gray;
        border-radius: 5px;
        padding: 3px 18px;
        cursor: pointer;
        background-color: #f5f5f5;
        transition: background-color 0.2s;
    }
    button:hover {
        background-color: #e0e0e0;
    }
</style>

---
layout: center
---

### Для чего такое может использоваться в Telegram-ботах?

<v-clicks>

- Анкеты, сбор личных данных
- Опросы, тесты
- Сбор отзывов
- Обратная связь, возможность для публики писать сообщения администраторам
- Для того, чтоб дать возможность администратору вносить данные в БД

</v-clicks>

---
layout: center
---

<h3> Как бы это выглядело в чате с Telegram ботом </h3>
<v-click>
    <img src="/images/1.png" class="w-full" />
</v-click>

---
layout: center
layoutClass: gap-16
---

Как сделать правильно:
![](/images/2.png)

---
layout: two-cols
layoutClass: gap-16
---

Состояния:

<ul>
<v-click at=1> <li> Имя </li> </v-click>
<v-click at=4> <li> Возраст </li> </v-click>
<v-click at=7> <li> Пол </li> </v-click>
<v-click at=10> <li> Любимый жанр </li> </v-click>
</ul>

::right::

Вопросы-ответы:

<ul class="answers">
  <v-click at=2><li>Как вас зовут? </li></v-click>
  <v-click at=3><li>Antonio </li></v-click>
  <v-click at=5><li>Сколько вам лет? </li></v-click>
  <v-click at=6><li>25 </li></v-click>
  <v-click at=8><li>Ваш пол? </li></v-click>
  <v-click at=9><li>Мужской</li></v-click>
  <v-click at=11><li>Ваш любимый жанр книг? </li></v-click>
  <v-click at=12><li>Фантастика</li></v-click>
</ul>

<style>
    ul.answers {
        list-style-type: none;
    }
    .answers li:nth-child(odd) {
        background-color: #f0f0f0;
    }
    .answers li:nth-child(even) {
        text-align: right;
    }
</style>

---

## Вопросы для проверки

<!-- - для чего диалоги в тг
- какой механизм используется для диалогов в айограм
- что такое states group
- как переключить состояние
- как написать декоратор для обработчика ответа пользователя при определенном состоянии
- как сохранить ответ пользователя во время диалога
- как получить все сохраненные во время диалога ответы пользователя -->


<Questions 
    :questions="[
        {
            q: 'Для чего используются диалоги в Telegram?',
            a: [
                'Для сбора информации',
                'Для общения',
                'Не знаю'
            ],
            correct: 0
        },
        {
            q: 'Какой механизм используются для диалогов в Aiogram?',
            a: [
                'Модульная архитектура',
                'Dialogue',
                'FSM - Finite State Machine',
                'Router',
                'Не знаю'
            ],
            correct: 2
        },
        {
            q: 'Что такое States Group?',
            a: [
                'Модульная архитектура',
                'Специальный роутер',
                'Класс для хранения состояний в виде полей',
                'Не знаю'
            ],
            correct: 2
        },
        {
            q: 'Как переключить состояние? ',
            a: [
                'state.set(Dialogue.user_name)',
                'state.set_state(Dialogue.user_name)',
                'Dialogue.user_name.set()'
            ],
            correct: 1
        },
        {
            q: 'Как написать декоратор для обработчика ответа пользователя при определенном состоянии? Например \'Dialogue.user_name?\'',
            a: [
                '@router.message(Dialogue.user_name?)',
                '@router.message(Dialogue.user_name)',
                '@router.message(state=Dialogue.user_name)',
                '@router.message()'
            ],
            correct: 1
        },
        {
            q: 'Как сохранить ответ пользователя во время диалога?',
            a: [
                'Dialogue.user_name = message',
                'state.set(Dialogue.user_name = message)',
                'state.update_data(user_name=message.text)',
                'user_name = message.text'
            ],
            correct: 2
        },
        {
            q: 'Как получить все сохраненные во время диалога ответы пользователя?',
            a: [
                'Dialogue.user_name',
                'state.get(Dialogue.user_name)',
                'state.get_data()',
                'message.text'
            ],
            correct: 2
        }
    ]"
/>