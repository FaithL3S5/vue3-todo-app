<script setup lang="ts">
import { ref, onMounted, computed, watch } from "vue";

interface Todo {
  content: string;
  done: boolean;
  createdAt: number;
}

// State variables
const todos = ref<Todo[]>([]);
const name = ref<string>("");
const input_content = ref<string>("");
const colorMode = ref<string>("light");
const sortOrder = ref<string>("asc");
const showDoneOnly = ref<boolean>(false);
const showNotDoneOnly = ref<boolean>(false);

// Toggles the sorting order between ascending and descending
const toggleSorting = () => {
  sortOrder.value = sortOrder.value === "asc" ? "des" : "asc";
};

// Computed property for sorting todos
const sortedTodos = computed(() => {
  const sorted = [...todos.value];
  return sorted.sort((a, b) => {
    // This will sort by done status (incomplete first)
    // if (a.done !== b.done) {
    //   return a.done ? 1 : -1;
    // }

    // Then sort by createdAt timestamp
    return sortOrder.value === "asc"
      ? a.createdAt - b.createdAt
      : b.createdAt - a.createdAt;
  });
});

// Computed property for filtering todos based on checkbox selections
const filteredTodos = computed(() => {
  let filtered = sortedTodos.value;
  if (showDoneOnly.value) {
    filtered = filtered.filter((todo) => todo.done);
  } else if (showNotDoneOnly.value) {
    filtered = filtered.filter((todo) => !todo.done);
  }
  return filtered;
});

// Toggles between light and dark color modes
const toggleColorMode = () => {
  colorMode.value = colorMode.value === "light" ? "dark" : "light";
  localStorage.setItem("colorMode", colorMode.value);
  document.body.classList.toggle("dark-mode", colorMode.value === "dark");
};

// Adds a new todo item to the list
const addTodo = () => {
  if (input_content.value.trim() === "") {
    return;
  }
  todos.value.push({
    content: input_content.value,
    done: false,
    createdAt: new Date().getTime(),
  });
  input_content.value = "";
};

// Removes a todo item from the list
const removeTodo = (todo: Todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

// Load initial data and set up watchers
onMounted(() => {
  name.value = localStorage.getItem("name") || "";
  todos.value = JSON.parse(localStorage.getItem("todos") || "[]");
  const savedColorMode = localStorage.getItem("colorMode");
  if (savedColorMode) {
    colorMode.value = savedColorMode;
    document.body.classList.toggle("dark-mode", colorMode.value === "dark");
  }
});

watch(name, (newVal) => {
  localStorage.setItem("name", newVal);
});

watch(
  todos,
  (newVal) => {
    localStorage.setItem("todos", JSON.stringify(newVal));
  },
  { deep: true }
);
</script>

<template>
  <main class="app" :class="{ 'dark-mode': colorMode === 'dark' }">
    <section class="greeting">
      <h2 class="title">
        Hello,
        <input type="text" placeholder="Name here" v-model="name" />
        <span @click="toggleColorMode">
          Theme: {{ colorMode.toUpperCase() }}
        </span>
      </h2>
      <h4 style="margin-top: 0.5em">
        You can change your username by clicking on it
      </h4>
    </section>

    <section class="create-todo">
      <h3>CREATE TODO</h3>
      <form @submit.prevent="addTodo">
        <h4>What are you gonna do?</h4>
        <input
          type="text"
          placeholder="e.g. buy some toothpaste"
          v-model="input_content"
        />
        <input type="submit" value="Add todo" />
      </form>
    </section>

    <section class="todo-list">
      <h3>
        TODO LIST - Click The ToDos Title to Edit
        <span class="filters" style="float: right">
          <label>
            <input type="checkbox" v-model="showDoneOnly" />
            <span class="bubble check personal"></span>
            Show Done Only
          </label>
          <label>
            <input type="checkbox" v-model="showNotDoneOnly" />
            <span class="bubble check personal"></span>
            Show Not Done Only
          </label>
          <span class="sort-toggle" @click="toggleSorting">
            Sorted: {{ sortOrder.toUpperCase() }} by time
          </span>
        </span>
      </h3>
      <div class="list">
        <h4 v-if="filteredTodos.length === 0">No todos for now..</h4>
        <div
          v-else
          v-for="todo in filteredTodos"
          :key="todo.createdAt"
          :class="`todo-item ${todo.done && 'done'}`"
        >
          <label>
            <input type="checkbox" v-model="todo.done" />
            <span :class="`bubble check`"></span>
          </label>

          <div class="todo-content">
            <input
              style="font-weight: bold; margin-top: 0.4rem"
              type="text"
              v-model="todo.content"
            />
            <h4 style="margin-top: 0.3rem">
              Created at: {{ new Date(todo.createdAt).toLocaleString() }}
            </h4>
          </div>

          <div class="actions">
            <button class="delete" @click="removeTodo(todo)">Delete</button>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>
