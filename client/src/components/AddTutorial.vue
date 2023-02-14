<template>
    <div class="submit-form">
      <div v-if="!submitted">
        <div class="form-group">
          <label for="title">Título</label>
          <input
            type="text"
            class="form-control"
            id="title"
            required
            v-model="tutorial.title"
            name="title"
          />
        </div>
  
        <div class="form-group">
          <label for="description">Descrição</label>
          <input
            class="form-control"
            id="description"
            required
            v-model="tutorial.description"
            name="description"
          />
        </div>
  
        <button @click="saveTutorial" class="btn btn-success">Enviar</button>
      </div>
  
      <div v-else>
        <h4>Adicionado com sucesso!</h4>
        <button class="btn btn-success" @click="newTutorial">Add</button>
      </div>
    </div>
  </template>
  
  <script>
  import TutorialDataService from "../services/TutorialDataService";
  export default {
    name: "add-tutorial",
    data() {
      return {
        tutorial: {
          id: null,
          title: "",
          description: "",
          published: false
        },
        submitted: false
      };
    },
    methods: {
      saveTutorial() {
        var data = {
          title: this.tutorial.title,
          description: this.tutorial.description
        };
        TutorialDataService.create(data)
          .then(response => {
            this.tutorial.id = response.data.id;
            console.log(response.data);
            this.submitted = true;
          })
          .catch(e => {
            console.log(e);
          });
      },
      
      newTutorial() {
        this.submitted = false;
        this.tutorial = {};
      }
    }
  };
  </script>
  
  <style>
  .submit-form {
    max-width: 300px;
    margin: auto;
  }
  </style>
  