<template>
  <div class="navbar is-success">
    <nav class="navbar is-success">
      <h1 class="is-size-2">Todo App</h1>
    </nav>
  </div>

  <div class="content mt-5">
    <form @submit.prevent="addTodo">
      <div class="field">
        <div class="control">
          <input
            v-model="todo"
            class="input is-rounded"
            type="text"
            placeholder="Örn. Koşuya Çıkılacak"
          />
        </div>
      </div>
      <div class="buttons mt-5">
        <button
          class="button is-success is-rounded is-normal is-fullwidth mx-6"
        >
          Ekle
        </button>
      </div>
    </form>
    <div v-for="todo in todos" :key="todo.id" class="card card my-5 mx-5">
      <div class="card-content">
        <div class="media">
          <div class="media-left"></div>
          <div class="media-content">
            <p
              :class="{ done: todo.done }"
              @click="done(todo)"
              class="title is-4 cursor"
            >
              {{ todo.content }}
            </p>
            <p class="subtitle is-6">Yapıldı mı : {{ todo.kontrol }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const todo = ref("");
    const todos = ref([]);

    function addTodo() {
      todos.value.push({
        done: false,
        content: todo.value,
        id: Date.now(),
        kontrol: "Hayır",
      });
      todo.value = "";
    }

    function done(todo) {
      todo.done = !todo.done;

      if (todo.done == true) {
        todo.kontrol = "Evet";
      } else {
        todo.kontrol = "Hayır";
      }
    }

    return {
      todo,
      todos,
      addTodo,
      done,
    };
  },
};
</script>

<style lang-scss>
.cursor {
  cursor: pointer;
}
.done {
  text-decoration: line-through;
}
</style>
