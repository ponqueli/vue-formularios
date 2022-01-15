<template>
  <div id="app">
    <div class="bg-secondary text-dark bg-opacity-25 p-3 border">
      <div class="container ">
        <h1 class="display-4 fw-bold">Formulários no Vue</h1>
        <p class="lead">Treinando a manipulação de formulários</p>
      </div>
    </div>

    <div class="container ">

      <div class="row">

        <!-- formulario -->
        <div class="col-sm-6">
          <h3>Preencha abaixo</h3>

          <form @submit.prevent="enviar" @reset="resetar">

            <div class="form-group">
              <label>Nome:</label>
              <input 
                type="text" 
                class="form-control" 
                placeholder="Seu nome"
                v-model.lazy.trim="desenvolvedor.nome">
            </div>

            <div class="form-group">
              <label>Endereço de email:</label>
              <input 
                type="email" 
                class="form-control" 
                placeholder="Seu email"
                v-model.lazy="desenvolvedor.email">
            </div>

            <div class="form-group">
              <label>Idade:</label>
              <input 
                type="number" 
                class="form-control" 
                placeholder="Sua idade"
                v-model.number="desenvolvedor.idade">
            </div>

            <div class="form-group">

              <p>Gênero:</p>

              <div class="form-check form-check-inline">
                <input 
                  type="radio" 
                  class="form-check-input" 
                  value="Masculino"
                  v-model="desenvolvedor.genero">
                <label class="form-check-label">Masculino</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="radio" 
                  class="form-check-input" 
                  value="Feminino"
                  v-model="desenvolvedor.genero">
                <label class="form-check-label">Feminino</label>
              </div>

            </div>

            <div class="form-group">
              <label>Ocupação:</label>
              <select 
                class="form-control" 
                v-model="desenvolvedor.ocupacao">
                <option value="" disabled>Selecione uma opção...</option>
                <option 
                  v-for="(ocupacao, indice) in ocupacoes"
                  :key="indice"
                  :value="ocupacao"> 
                    {{ ocupacao }}
                </option>
              </select>
            </div>  

            <div class="form-group">
              <p>Tecnologias:</p>
              <div class="form-check form-check-inline">
                <input 
                  type="checkbox" 
                  class="form-check-input" 
                  value="JavaScript"
                  v-model="desenvolvedor.tecnologias">
                <label class="form-check-label">JavaScript</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox" 
                  class="form-check-input"
                  value="Vue JS"
                  v-model="desenvolvedor.tecnologias">
                <label class="form-check-label">Vue JS</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox" 
                  class="form-check-input" 
                  value="Vuex"
                  v-model="desenvolvedor.tecnologias">
                <label class="form-check-label">Vuex</label>
              </div>

              <div class="form-check form-check-inline">
                <input 
                  type="checkbox" 
                  class="form-check-input" 
                  value="Vue Router"
                  v-model="desenvolvedor.tecnologias">
                <label class="form-check-label">Vue Router</label>
              </div>
            </div>      

            <div class="form-group">
              <label>Resumo de perfil:</label>
              <textarea 
                class="form-control" 
                placeholder="Conte-nos um pouco sobre você..."
                v-model.lazy.trim="desenvolvedor.resumo">
              </textarea>
            </div>

            <div class="form-group">
              <AppRange
                label="Salário pretendido:"
                :inputClassesLabel="[{'form-label': true }]"
                :inputClassesInput="[{ 'form-range': true }]"
                v-model.number="desenvolvedor.salario"
                min="1000"
                max="15000"
                step="500"/>
            </div>

            <div class="form-group">
              <div class="form-check form-check-inline">
                <input 
                  type="checkbox" 
                  class="form-check-input"
                  v-model="desenvolvedor.notificacoes"
                  true-value="Sim"
                  false-value="Não">
                <label class="form-check-label">Receber notificações por email</label>
              </div>
            </div>

            <button class="btn btn-secondary" type="reset">Resetar</button>
            <button class="btn btn-success" type="submit">Enviar</button>
          </form>
        </div>

        <!-- saida -->
        <div class="col-sm-6">
          <h3>Saída</h3>
          <div class="card">
            <div class="card-header">Dados</div>
            <ul class="list-group list-group-flush">
              <li class="list-group-item"><strong>Nome:</strong>{{ desenvolvedor.nome }}</li>
              <li class="list-group-item"><strong>Email:</strong> {{ desenvolvedor.email }} </li>
              <li class="list-group-item"><strong>Idade:</strong>{{ desenvolvedor.idade }}</li>
              <li class="list-group-item"><strong>Gênero:</strong> {{ desenvolvedor.genero }}</li>
              <li class="list-group-item"><strong>Ocupação:</strong> {{ desenvolvedor.ocupacao }} </li>
              <li class="list-group-item">
                <strong>Tecnologias:</strong> 
                <ul v-for="(tecnologia,indice) in desenvolvedor.tecnologias"
                  :key="indice" 
                  class="nav flex-column">
                  <li class="nav-item">
                    {{tecnologia}}
                  </li>
                </ul>
              </li>
              <li class="list-group-item"><strong>Resumo:</strong>
                <div style="white-space: pre">{{ desenvolvedor.resumo }}</div> 
              </li>
              <li class="list-group-item"><strong>Receber notificações?</strong>{{ desenvolvedor.notificacoes }} </li>
              <li class="list-group-item"><strong>Salário pretendido: </strong>{{ desenvolvedor.salario }} </li>
            </ul>

            <div class="card-header">Model</div>
            <div class="card-body">
              <pre><code>{{ desenvolvedor }}</code></pre>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import AppRange from './components/Range.vue'

export default {
  components:{
    AppRange
  },
  data(){
    return {
      desenvolvedor: {},
      valoresPadroes:{
        nome:'',
        email:'',
        idade: 31,
        resumo:'',
        genero: 'Masculino',
        notificacoes: 'Não',
        tecnologias:[],
        ocupacao: '',
        salario: 7000
      },
      ocupacoes:[
        'Desenvolvedor Front End (web)',
        'Desenvolvedor Front End (mobile)',
        'Desenvolvedor Front End (web e mobile)',
        'Desenvolvedor Back End',
        'Desenvolvedor Full Stack'
      ]
    }
  },
  methods:{
    enviar(){
      const formularioEnviado = {...this.desenvolvedor}
      console.log("Formulário enviado: ", formularioEnviado)
    },
    resetar(){
      this.desenvolvedor = { ...this.valoresPadroes }
    }
  },
  created(){
    this.resetar();
  }
}
</script>

<style scoped>
  .btn {
    margin-right: 5px;
  }
</style>