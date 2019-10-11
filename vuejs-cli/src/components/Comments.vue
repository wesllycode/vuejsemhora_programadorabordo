<template>
  <div class="container">
    <h1> Comentários </h1>
    <hr />
    <!-- Aqui v-on: para pegar ação nesse caso vou pegar o que criei emit pegar toda ação passado por la 
         Criei um componente para formulário para ambos conversarem
    -->
    <FormTodo v-on:add-todo="addComment"></FormTodo>    
      <div class="list-group">
      <p v-if="comments.length <= 0"> Sem comentários... </p>
        <!-- aqui estava dando um erro por causa  v-bind:key | È uma diretiva ligação de dados com template com a parte do view, algoritmo vai aplicar mudanças. Para facilitar a vida dele quando tiver interação de lista algo do tipo eu coloque uma chave única para ajuda o vue identificar as mudanças, o usei o index porque ele pega numero da variável -->
        <div class="list-group-item" v-for="(comment, index) in allComments" v-bind:key="index">
          <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
         <p>{{ comment.message }}</p>
         <div>
          <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
        </div>
      </div>
    </div>
      <hr />
  </div>  
</template>

<script>
import FormTodo from './FormTodo';
export default {
  components:{
    FormTodo
  },
  data() {
        return {
          // Aqui deixo vazio comentário, para ele começcar vazio
           comments: []          
        }
      },
        methods: { 
        addComment(comment) {
          this.comments.push(comment);
        },         
        removeComment(index){
          this.comments.splice(index, 1);
       }               
      },
      // Computed é bom pois não preciso colocar esse lógica direto no meu template
      computed: {
        allComments(){
          return this.comments.map(comment => ({
            ...comment,
            name: comment.name.trim() === '' ? 'Anônimo' : comment.name
          }))
        }
      },
      // Consigo monitorar as atividades e  a partir da ai tomar uma ação
      // Ele bom para salvar no banco dados, quando deletou, quando atualizou e assim vai
      watch: {
        comments(val){
          console.log('val', val);
        }
      } 
  }
</script>