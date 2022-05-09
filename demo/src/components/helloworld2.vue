<template>
  <div class="hello">
  <div class = "container">
    <h2>Categorias</h2>
    <button type="button" class = "btn-primary" @click="allCategories">Mostrar categorias</button>

    <div v-for = "c in categorias">
      <div class = "row">
        <p>{{c.name}}</p>
      </div>
    </div>
  </div>
  </div>
</template>

<script>
  import axios from 'axios'

export default {
  name: 'helloworld2',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      userName:'',
      age:'',
      keywords:'',
      categorias:[]
  }
},
    methods:{
        addUser(){ //
            let name = this.userName;
            let age = this.age;
            axios.post('/api/user/addUser',{
                name,age
            }).then(res=>{
                alert('Información agregada correctamente');
            }).catch(err=>{
                console.log(err)
            })
        },
        selectUser(){
            let name = this.keywords;
            axios.post('api/user/selectUser',{
                name
            }).then(res=>{
                let data = res.data[0];
                this.userName = data.name;
                this.age = data.age
            }).catch(err=>{
                console.log(err)
            })
        },
        allCategories(){
          axios.post('api/user/allCategories', {
          }).then(res => {
            console.log(res.data);
            this.categorias = res.data;
          })
        }
  }
}
</script>


<style scoped>
h1 {
  font-weight: normal;
}
</style>

