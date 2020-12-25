<template>
  <div id="app">
    <h3>{{titulo}}</h3>
    <div class="form">
      <div class="form-group">
        <label>Título:</label>
        <input class="form-control" type="text" name="titulo" id="titulo" v-model="nota.titulo">
      </div>
      <div class="form-group">
        <label for="">Texto:</label>
        <textarea class="form-control"  v-model="nota.texto"></textarea>
      </div>
      <button class="btn btn-primary" @click="agregarNota">Enviar</button>
    </div>
    <hr>
    <div class="col-sm-12">
      <div class="col-sm-4 nota" v-for="(n ,key) in notas" :key="key">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{n.titulo}}</h5>
              <p class="card-text">{{n.texto}}</p>
              <p class="card-text">{{n.fecha}}</p>
            </div>
            <button @click.stop="eliminarNota(key)">x</button>
          </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      titulo: 'Gestión de notas',
      nota:{
        titulo:'',
        texto:''
      },
      notas:[
        {
          titulo: 'Ir al cine',
          texto: 'Examinar la cartelera',
          fecha: new Date(Date.now()).toLocaleDateString(),
        }
      ],
    }
  },
  methods:{
    agregarNota(){
      let {texto, titulo} = this.nota;
      this.notas.push({
        texto,
        titulo,
        fecha: new Date(Date.now()).toLocaleDateString()
      });
      this.nota = {
        titulo: '',
        texto: ''
      }
    },
    eliminarNota(index){

      this.notas.splice(index);
      this.nota = {
        titulo: '',
        texto: ''
      }
    }
  }
}
</script>

<style>

  .form{
    text-align: left;
  }
  .card{
    text-align: left;
    border: 1px solid grey;
    border-radius: 3px;
    padding-left: 8px;
    padding-right: 8px;
  }
  .nota{
    padding: 5px;
  }
  .btn{
    margin-top: 10px;
  }
</style>
