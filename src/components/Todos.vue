<template>
  <!-- Container -->
  <div
    class="transition-all duration-500 w-full flex justify-center items-center flex-col h-full"
  >
    <div
      class="topContainer w-full sticky top-0 left-0 z-10 text-center bg-gray-800 pt-20 pb-3"
    >
      <!-- Title -->
      <h1 class="font-bold text-7xl text-green-300">Todo App</h1>
      <!-- Add Todo Container -->
      <div class="input my-12 w-full px-14 lg:px-56 flex flex-wrap">
        <input
          class="w-full lg:w-4/5 py-3 px-8 outline-none border-none"
          type="text"
          placeholder="Type a Todo . . ."
          v-model="newTodo"
        />
        <button
          class="w-full lg:w-1/5 cursor-pointer bg-green-500 text-white font-bold py-3 px-8"
          @click="addTodo()"
        >
          Add Todo
        </button>
      </div>
    </div>
    <!-- Todo's Container -->
    <ul class="w-full px-14 lg:px-56">
      <!-- Todos -->
      <li
        class="bg-green-50 rounded-2xl w-full py-4 pl-6 pr-9 my-4 font-bold text-xl relative"
        v-for="(index, Todo) in Todos"
        :key="Todo.id"
      >
        {{ Todo + 1 }} - {{ index }}

        <!-- Icon Box -->
        <div class="absolute right-3 top-2 mt-2 px-3 bg-green-50">
          <!-- Check Icon -->
          <box-icon
            type="solid"
            class="cursor-pointer mr-3"
            @click="removeTodo(index)"
            name="check-circle"
            color="green"
            with="36"
          ></box-icon>
          <!-- Remove Icon -->
          <box-icon
            name="trash"
            color="gray"
            class="cursor-pointer"
            @click="removeTodo(index)"
          ></box-icon>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
// Import BoxIcons
import "boxicons";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Todos",
  data() {
    return {
      newTodo: "",
      // Default Todo's
      Todos: ["First Todo . . ."],
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo == "") {
        this.newTodo = "Nothing to do . . .";
      } else {
        // Push New Todo To Todos List
        this.Todos.push(this.newTodo);
        // Save Todo In Local Storage
        localStorage.setItem("Todos", JSON.stringify(this.Todos));
        // Clear Input
        this.newTodo = "";
      }
    },
    removeTodo(index) {
      // Remove Todo by Index
      this.Todos.splice(index, 1);
      // Remove Todo From Local Storage
      localStorage.setItem("Todos", JSON.stringify(this.Todos));
    },
  },
  created: function () {
    // Get Todos From Local Storage
    this.Todos = JSON.parse(localStorage.getItem("Todos"));
    // Assign Todo's To Todos List
    this.Todos = this.Todos || [];
  },
};
</script>
