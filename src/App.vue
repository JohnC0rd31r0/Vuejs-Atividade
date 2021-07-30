<template>
  <body>
    <div id="app" class="container w-100">
        <h2 class="mt-4">{{ titulo }}</h2>
        <main class="container">
            <div class="row">
                <div class="col-sm-8 w-75">
                    <div class="col-sm-8 g-1 pt-3 ms-2">
                        <input class="mb-4 form-control border-2  border-info" type="text" v-model="novoNome"
                            placeholder="Nome">
                        <input class="w-50 border-2 border-info" type="date" v-model="novaData">
                        <div class="col mt-4 p-2">
                            <input type="checkbox" v-model="novoStatus">
                            <label>  Aprovado</label>
                        </div>
                    </div>
                    <div class="row g-2 w-75 ">
                        <input @keyup.enter="adicionarTarefa" class="form-control border-2 border-info ms-2 col"
                            type="email" v-model="novoEmail" placeholder="john@example.com">
                        <span class="input-group-btn mt-4 ms-1">
                            <button @click="adicionarTarefa" class="btn btn-primary">Adicionar</button>
                        </span>
                    </div>
                </div>
                <div class="imagem col-sm w-25 mx-auto">
                    <img src=".\assets\professor.png" alt="professor">
                </div>
            </div>
        </main>
        <div class="container">
        <ul>
            <br>
            <li v-for=" (tarefa, index) in tarefas" :key="index"
                class="list-group-item w-75 border-2 border-info rounded lista m-2">

                <label>
                    <p><em>Nome:</em> {{ tarefa.titulo }}</p>
                    <p><em>Email:</em> {{tarefa.email}}</p>
                    <p><em>Nascimento:</em> {{tarefa.tempo}}</p>
                    <p><em>Status:</em> {{tarefa.status}}</p>
                </label>
            </li>
        </ul>
    </div>
        <div class="container">
            <div class="row">
                <p class="col m-2">Total de Alunos: <span>{{totalAlunos}}</span></p>
                <p class="col m-2">Aprovados: <span>{{totalAprovados}}</span></p>
                <p class="col m-2">Reprovados: <span>{{totalReprovados}}</span></p>
            </div>
        </div>
        <footer class="pt-5">
            <hr>
            <b>
                <em>Joinville, 2021. John Cordeiro</em></b>
        </footer>
    </div>

</body>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      titulo: "Alunos:",
      tarefas: [
        {
          titulo: "John",
          tempo: "00 / 00 / 0000",
          email: "joãosilva@gmail.com",
          status: "Aprovado",
        },
      ],
      novoNome: "",
      novaData: "",
      novoEmail: "",
      novoStatus: "",
    };
  },
  methods: {
    adicionarTarefa() {
      this.tarefas.push({
        titulo: this.novoNome,
        tempo: organizar(this.novaData),
        email: this.novoEmail,
        status: passoudeAno(this.novoStatus),
      });
      this.novoNome = "";
      this.novaData = "";
      this.novoEmail = "";
      this.novoStatus = "";

      function organizar(data) {
        return data.split("-").reverse().join("/");
      }
      function passoudeAno(status) {
        if (status === true) {
          return "Aprovado";
        } else return "Reprovado";
      }
    },
  },
  computed: {
    totalAlunos() {
      return this.tarefas.length;
    },
    totalAprovados() {
      const aprovados = this.tarefas.filter(
        (tarefa) => tarefa.status === "Aprovado"
      );
      return aprovados.length;
    },
    totalReprovados() {
      return this.totalAlunos - this.totalAprovados;
    },
  },
};

</script>

<style>
  imagem {
    position: relative;
    float: right;
  }
</style>
