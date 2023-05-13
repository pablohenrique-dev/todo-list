<template>
  <section>
    <div class="container">
      <form>
        <input
          type="text"
          placeholder="Descrição da tarefa"
          v-model="message"
        />
        <button @click.prevent="adicionarTask">Adicionar</button>
      </form>
      <ul class="tarefas" v-if="tarefas.length > 0">
        <li
          :class="{ concluida: tarefa.finalizada }"
          class="tarefa"
          v-for="(tarefa, index) in tarefas"
          :key="index"
        >
          <button class="finalizar" @click="() => atualizarTask(index)">
            &times;
          </button>
          <p>
            {{ tarefa.descricao }}
          </p>
          <div class="botoes">
            <button @click="() => editarTask(index)" class="editar">
              Editar
            </button>
            <button @click="() => deletarTask(index)" class="excluir">
              Remover
            </button>
          </div>
        </li>
        <button @click="removeAll" class="removeAll">
          Remover todas as tarefas
        </button>
      </ul>
      <div v-else>
        <h2>Adicone tarefas</h2>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "ToDoList",
  data() {
    return {
      tarefas: [],
      message: "",
      isEditing: false,
      currentId: null,
    };
  },
  methods: {
    removeAll() {
      const confirmar = confirm("Deseja mesmo remover todas as tarefas?");
      if (confirmar) {
        window.localStorage.removeItem("task");
        this.tarefas = [];
      }
    },
    adicionarTask() {
      if (this.message) {
        if (this.isEditing) {
          this.tarefas[this.currentId].descricao = this.message;
          this.message = "";
          this.isEditing = false;
          this.adicionarLocalStorage();
        } else {
          this.tarefas.push({
            descricao: this.message,
            finalizada: false,
          });
          this.message = "";
          this.adicionarLocalStorage();
        }
      }
    },
    editarTask(index) {
      this.message = this.tarefas[index].descricao;
      this.tarefas[index].finalizada = false;
      this.isEditing = true;
      this.currentId = index;
    },
    adicionarLocalStorage() {
      window.localStorage.task = JSON.stringify(this.tarefas);
    },
    atualizarTask(index) {
      this.tarefas[index].finalizada = !this.tarefas[index].finalizada;
      this.adicionarLocalStorage();
    },
    deletarTask(index) {
      this.tarefas.splice(index, 1);
      this.adicionarLocalStorage();
    },
    lerLocalStorage() {
      if (window.localStorage.task) {
        const db = JSON.parse(window.localStorage.task);
        db.forEach((item) => {
          this.tarefas.push(item);
        });
      }
    },
  },
  created() {
    this.lerLocalStorage();
  },
};
</script>

<style scoped>
form {
  width: 100%;
  margin-bottom: 8px;
  display: flex;
  justify-content: space-between;
}

div h2 {
  margin-top: 16px;
}
.concluida p {
  text-decoration: line-through;
}

form input {
  width: 80%;
  height: 32px;
  padding: 0 16px;
  border: 1px solid #bdc4c9;
}

form input:focus {
  outline: 1px solid #9da4a9;
}

form button {
  border: 1px solid #bdc4c9;
  width: 18%;
  height: 32px;
  background: #02b068;
  color: white;
  font-weight: 600;
}
.container {
  widows: 100%;
  width: 500px;
  margin: 0 auto;
  border: 1px solid #bdc4c9;
  padding: 16px;
}

.tarefas {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.tarefa + .tarefa {
  margin-top: 8px;
}
.tarefa {
  width: 100%;
  display: flex;
  gap: 8px 16px;
  justify-content: space-between;
  align-items: center;
  background: #eef2f5;
  padding: 8px 16px;
  border: 1px solid #bdc4c9;
}

.concluida .finalizar {
  background: #1582e8;
  border: 1px solid #1582e8;
}

.finalizar {
  border: 1px solid #bdc4c9;
  background: #ffffff;
  color: #ffffff;
  padding: 2px 6px;
}

.excluir,
.editar {
  padding: 6px 6px;
}

.editar {
  background: #1582e8;
  border: none;
  color: #ffffff;
  margin-right: 8px;
}

.removeAll {
  width: 100%;
  margin-top: 8px;
  padding: 12px 0;
  border: none;
  background: #ee414c;
  color: #ffffff;
  font-weight: 600;
}

.excluir {
  background: #ee414c;
  border: none;
  color: white;
}

.excluir:hover {
  background: #c81117;
}
</style>