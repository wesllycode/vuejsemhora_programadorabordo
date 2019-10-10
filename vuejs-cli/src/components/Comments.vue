<template>
  <div class="container">
    <h1> Comentários </h1>
    <hr />
    <div class ="form-todo form-group">
      <p>
          <input placeholder="nome" type="text" name="author" class="form-control" v-model="name" />
      </p>
      <p>
        <textarea placeholder="Comentário" name="message" class="form-control" v-model="message"></textarea>
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
      <div class="list-group">
        <div class="list-group-item" v-for="(comment, index) in allComments">
          <span class="comment__author">Autor: <strong>{{ comment.name }}</strong></span>
         <p>{{ comment.message }}</p>
         <div>
          <a href="#" title="Excluir" v-on:click.prevent=" removeComment(index)">Excluir</a>
        </div>
      </div>
      <hr />
  </div> 
  </div>
</template>

<script>
export default {
  data() {
        return {
          // Aqui deixo vazio comentário, para ele começcar vazio
           comments: [],             
           name: '',
           message: ''
            }
      },
        methods: {
          addComment() {
           
            this.comments.push({
              name: this.name,
              message: this.message
           });
           // Assim que ele comentar, vai apagar os campos para ficar vazio
           this.name = '';
           this.message = '';
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