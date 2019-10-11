<template>
  <div class ="form-todo form-group">
      <p>
          <input placeholder="nome" type="text" name="author" class="form-control" v-model="name" />
      </p>
      <p>
        <textarea placeholder="Comentário" name="message" class="form-control" v-model="message"></textarea>
      </p>
      <button v-on:click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>
<script>
export default {
  data() {
    return {
      name: '',
      message: ''
    }
  },
  methods:{
  addComment() {           
           if(this.message.trim() == ''){
             return;
           } 
            // Quando clico no botão ele aciona esse evento add-todo passando comentario  para componente que criei no Comments.vue
           this.$emit('add-todo', {
             name: this.name,
             message: this.message,
           });
           // Assim que ele comentar, vai apagar os campos para ficar vazio
           this.name = '';
           this.message = '';
     }
  }
}
</script>