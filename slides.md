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
        <input class="w-full border border-gray-500 rounded px-2" type="text" placeholder="Ваша любимая книга" />
    </form>
</div>
</v-click>

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
