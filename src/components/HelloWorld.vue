<template>
  <div id="app">
      
      <img v-bind:src="require('../../static/fondo.png')" alt="">
      <h1 class="text-success">Prueba tecnica de desarrollo EEP</h1>
      <h2>Ingrese indentificación del empleado</h2>
      
      <input type="number" placeholder="Identificacion" v-model="ident">
      <button @click="consultar">Obtener empleados</button><br>
      
      <h2>Empleados</h2>
      <table>
        <thead>
          <tr>
            <th scope="col">Id</th>
            <th scope="col">Name</th>
            <th scope="col">contractTypeName</th>
            <th scope="col">roleId</th>
            <th scope="col">roleName</th>
            <th scope="col">roleDescription</th>
            <th scope="col">hourlySalary</th>
            <th scope="col">monthlySalary</th>
            <th scope="col">yearSalary</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="empleado in empleados2" v-bind:key="empleado.id">
            <th scope="row">{{ empleado.id }}</th>
            <td>{{ empleado.name }}</td>
            <td>{{ empleado.contractTypeName }}</td>
            <td>{{ empleado.roleId }}</td>
            <td>{{ empleado.roleName }}</td>
            <td>{{ empleado.roleDescription }}</td>
            <td>{{ empleado.hourlySalary }}</td>
            <td>{{ empleado.monthlySalary }}</td>
            <td>{{ empleado.monthlySalary*12 }}</td>
          </tr>
          <tr>
            <th scope="row">{{ id }}</th>
            <td>{{ name }}</td>
            <td>{{ contractTypeName }}</td>
            <td>{{ roleId }}</td>
            <td>{{ roleName }}</td>
            <td>{{ roleDescription }}</td>
            <td>{{ hourlySalary }}</td>
            <td>{{ monthlySalary }}</td>
            <td>{{ monthlySalary*12 }}</td>
          </tr>
        </tbody>
      </table> 
      <h2>Pablo Alejandro Perdomo</h2>
  </div>
</template>

<script>  
  import axios from 'axios'
  export default {
    name: 'app',
    
    data(){
      return {
        todos: null,
        empleados: null,
        empleados2: null,
        name: null,
        id: null,
        contractTypeName: null,
        roleId: null,
        roleName: null,
        roleDescription:null,
        hourlySalary: null,
        monthlySalary: null,
        mensaje: 0,
        salario: null,
        ident: 0
      }
    },
      
    methods: {
      consultar(){
        axios.get('http://masglobaltestapi.azurewebsites.net/api/Employees')
        .then(response=>{
          this.empleados=response.data;
          const v = this.ident;
          
          if(v>0){
            const a = this.empleados.length;
            const b = this.empleados[v-1].name;

            for(let i=0;i<a;++i){
              
              if(v == this.empleados[i].roleId){

                this.id = this.empleados[i].id;
                this.name = this.empleados[i].name;
                this.contractTypeName = this.empleados[i].contractTypeName;
                this.roleId = this.empleados[i].roleId;
                this.roleName = this.empleados[i].roleName;
                this.roleDescription = this.empleados[i].roleDescription;
                this.hourlySalary = this.empleados[i].hourlySalary;
                this.monthlySalary = this.empleados[i].monthlySalary;
                i = i + 2;
              }
            }
            this.empleados2 = null;
          }
          else{
            this.empleados2 = this.empleados;
            this.id = null;
            this.name = null;
            this.contractTypeName = null;
            this.roleId = null;
            this.roleName = null;
            this.roleDescription = null;
            this.hourlySalary = null;
            this.monthlySalary = null;
          }
        }).catch(e => console.log(e));
      }
    }
  }
</script>

<style>
table {
    width:50%;
    text-align:left;
    margin: 0 auto;
}

table th {
    background-color:lightblue;
    font-size: 17px;
}

table td {
  font-size: 15px;
}

</style>
