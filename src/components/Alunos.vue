<template>
  <h2>Adicione Aluno</h2>
  <div class="container">
    <input v-model="nome" type="text">
  <input v-model="nota" type="number" id="nota">
  <button v-on:click="salvarAlunos" id="plus"><img src="../assets/plus.png" class="img-fluid" ></button>
    
  </div>
    <p id="erro" v-if="erro != ''">{{erro}}</p>

  <p v-if="alunos.length == 0">Lista vazia!</p>
    <p>Quantidade de pessoas:{{alunos.length}}</p>

  

  <div >
    <div v-if="alunos.length != 0">
      <p>Lista de alunos</p>
            <hr>

    </div>
    
    
    <ul v-for="aluno in alunos"> 
      <li v-if="aluno.length !=0">Nome:{{ aluno.nome }} 
 Nota:{{aluno.nota}}</li>
    </ul>
  </div>
  <div class="list-aprovados" >
     <div v-if="aprovados.length != 0">
      <p>Lista de alunos aprovados</p>
            <hr>

    </div>
   <ul v-for="aluno in aprovados"> 
      <li v-if="aluno.length !=0">Nome:{{ aluno.nome }} 
 Nota:{{aluno.nota}}</li>
    </ul>
  </div>
  <div >
     <div v-if="reprovados.length != 0">
      <p>Lista de alunos reprovados</p>
            <hr>

    </div>
   <ul v-for="aluno in reprovados"> 
      <li v-if="aluno.length !=0">Nome:{{ aluno.nome }} 
 Nota:{{aluno.nota}}</li>
    </ul>
  </div>

  <button v-if="alunos.length != 0" id="btn-limpar" v-on:click="limparAlunos"><img class="img-fluid" src="../assets/broom.png" >Limpar</button>
</template>

<script>
  export default{
   nome:'Alunos',

    data(){
      return {
        nome: '',
        nota: 0,
        alunos: [],
        aprovados: [],
        reprovados: [],
        erro: '',
        
      }
    },
     methods: {
       salvarAlunos(){
         if(this.nome == '' || this.nota<0 || this.nota>10){
           this.erro = "Valor invalido"
           
         }else{
           this.alunos.push({nome: this.nome , nota: this.nota});
           
           if(this.nota<7){
              this.reprovados.push({nome: this.nome , nota: this.nota});
           }else{
             this.aprovados.push({nome: this.nome , nota: this.nota});
           }
           this.nome = '';           
           this.nota = 0;
           this.erro = '';

           
         }
         },

       limparAlunos(){
         if(this.alunos.length != 0){
          this.alunos = []
          this.aprovados = []
          this.reprovados = []
           this.erro=''

           
         }
       }
      
    }
  }


</script>

<style>
  #plus{
    background-color:green;    
    border: 1px white;
    border-radius: 2px;
    align-items: center;
    
  }
  .img-fluid{
    width:14px;
    padding-top: 2px
    
  }
  .container{
    display: flex;
  }
  #nota{
    width:80px;
    margin-inline: 5px;
  }
  #erro{
    color: red;
  }
</style>