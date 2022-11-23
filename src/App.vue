<script setup>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup

import { onMounted, ref, watch } from "vue";

const todos = ref([]);
const name = ref("");
const input_content = ref("");

const addTodo = () => {
  if (input_content.value === "" || input_content.value === null) return;

  todos.value.push({
    id: todos.value.length + 1,
    content: input_content.value,
    isDone: false,
  });
  input_content.value = "";
};

const removeTodo = (id) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

watch(
  todos,
  (newValue) => {
    localStorage.setItem("todos", JSON.stringify(newValue));
  },
  { deep: true }
);
watch(name, (newValue) => {
  localStorage.setItem("name", newValue);
});

onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos")) || [];
});
</script>

<template>
  <main class="min-h-screen bg-background pt-5 px-5">
    <section>
      <h1 class="text-2xl text-white">
        What's Up,
        <input
          type="text"
          :class="`text-2xl text-white bg-background ${
            name ? '' : 'text-backgroundThin'
          }`"
          placeholder="Name Here"
          v-model="name"
        />
      </h1>
    </section>
    <div class="flex flex-col items-center">
      <section>
        <form
          @submit.prevent="addTodo"
          class="my-14 w-[660px] h-[70px] bg-backgroundThin flex items-center"
        >
          <input
            type="text"
            class="w-full h-full px-5 text-2xl border-none bg-backgroundThin text-white"
            placeholder="What needs to be done?"
            v-model="input_content"
          />
          <input
            type="submit"
            value="Add Todo"
            class="w-32 h-full font-extrabold text-xl bg-green text-white"
          />
        </form>
        <div v-for="todo in todos">
          <section>
            <div
              @click="
                `${
                  todo.isDone
                    ? removeTodo(todo.id)
                    : (todo.isDone = !todo.isDone)
                }`
              "
              class="h-20 px-6 py-5 bg-backgroundThin flex items-center"
            >
              <input
                type="text"
                v-model="todo.content"
                :class="`text-3x bg-backgroundThin  ${
                  todo.isDone ? 'text-blue' : 'text-white'
                }`"
              />
            </div>
            <hr />
          </section>
        </div>
      </section>
    </div>
  </main>
</template>
