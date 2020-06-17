<template>
  <div id="app">
    <div class="container">
      <nav class="navbar navbar-expand-sm bg-danger navbar-dark">
            <a class="navbar-brand" href="#">Магазин компьютеров
              </a>
            <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
                <span class="navbar-toggler-icon"></span>
              </button>

            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav mx-5">
                    <li class="nav-item active">
                        <a class="nav-link" href="#">Процессор</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="#">Материнская плата</a>
                    </li>
                    
                </ul>
            </div>
      </nav>
        <br>
        <h1> Каталог материнки</h1>
        <br>

    <div class="from-group">
      <label for=""> название</label>
      <input type="text" class="form-control" v-model="Model"/>
    </div>
<div class="from-group">
      <label for=""> частота</label>
      <input type="text" class="form-control" v-model="Mgc"/>
    </div>
<button class="btn btn-primary" @click="onSave"> добавить</button>
<br>
    <div class="row" v-for="note in mate" :key="note.id">
      <div class="col-4">{{note.Model}}</div>
      <div class="col-4">{{note.Mgc}}</div>
      <div class="col-4"><button class="btn btn-danger" @click="onDelete(note.id)"> Удалить </button>
    </div>
    <br>

    <br>
        <h1> Каталог процессоров</h1>
        <br>

    <div class="from-group">
      <label for=""> название процессара</label>
      <input type="text" class="form-control" v-model="name"/>
    </div>
<div class="from-group">
      <label for=""> частота</label>
      <input type="text" class="form-control" v-model="MgcgM"/>
    </div>
<button class="btn btn-primary" @click="onSaveOne"> добавить</button>
<br>
    <div class="row" v-for="note in mate" :key="note.id">
      <div class="col-4">{{note.name}}</div>
      <div class="col-4">{{note.MgcgM}}</div>
      <div class="col-4"><button class="btn btn-danger" @click="onDeleteOne(note.id)"> Удалить </button>
    </div>
    <div class="row" style="background-color:gray">
      <div class="col-sm-4">
        Борисовец Ульяна Бориосвна
        <br>
        181-362
      </div>
      <div class="col-sm-4">
       Дата сдачи
        <br>
        17.06.2020
      </div>
      <div class="col-sm-4">
       Материалы
        <br>
        <a href="" target="_blank"> HTML</a>
      </div>

    </div>
  </div>
    </div>
    </div>
  </div>
</template>

<script>


export default {
  name:'App',
data(){
  return{
    mate:[],
    Model: '',
      Mgc: '',
      process:'',
      name:'',
      MgcgM:''
  };
},
  components: {},
  methods:{
    async updateDate(){
      try{
        let res = await this.$http.get(" http://localhost:3000/mate");
        this.mate = await res.json();
      }catch(err){
        console.error(err);
      }
    },
    async onSave(){
      let note = {
        Model: this.Model,
        sum: this.Mgc
      };
      try {
        await this.$http.post("http://localhost:3000/mate", note);
        this.updateDate();

      }catch(err){
        console.error(err);
      }
    },
    async onDelete(id){
      try{
        await this.$http.delete("http://localhost:3000/mate/" + id);
        this.updateDelete();

      }catch(err){
        console.error(err);
      }

    },
    async updateDateOne(){
      try{
        let res = await this.$http.get(" http://localhost:3000/process");
        this.mate = await res.json();
      }catch(err){
        console.error(err);
      }
    },
    async onSaveOne(){
      let note = {
        name: this.name,
        MgcgM: this.MgcgM
      };
      try {
        await this.$http.post("http://localhost:3000/process", note);
        this.updateDateOne();

      }catch(err){
        console.error(err);
      }
    },
    async onDeleteOne(id){
      try{
        await this.$http.delete("http://localhost:3000/process/" + id);
        this.updateDeleteOne();

      }catch(err){
        console.error(err);
      }

  }
  
  },
  created(){
this.updateDate();
this.updateDateOne();
  },
  
};
</script>

<style>



    
    body{
      background-color: rgba(0, 174, 255, 0.534);
    }
    
</style>
