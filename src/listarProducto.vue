<template>
    <div class="container">
      <br>
      <h4 style="text-align:left; font-family:georgia"> <strong>Listar Productos </strong></h4>
      <br>
      <div class="col">
        <div class="row">
            <br><br><br><br>
            <!--Combobox-->
            <label for="select">Seleccione una categoria:</label>
            <br><br>
                  <div class="styled-select slate" style="margin-left: 10px">
                       <select  @change="seleccionarCategoria()" v-model="categoria_seleccionado">
                       <option value=0 disabled selected style="width: 100px; font-family: georgia">Seleccionar categoría</option>
                       <option
                           style="width: 100px; font-family: georgia"
                           v-for="categoria in categorias"
                           v-bind:key="categoria.nombreCategoria"
                           v-bind:value="categoria.nombreCategoria"> {{ categoria.nombreCategoria }}
                       </option>
                       </select>
                  </div>
            <br>
       </div>
       <br>
       <div class="row">
            <!--Lista de productos filtrados-->
            <ul class="list-group">
                <li v-for="producto in productos_filtrados"
                    style = "height: 50px; font-family: georgia; text-align: center"
                    class = "list-group-item"> {{ producto.nombreProducto}}  ${{ producto.precio}}
                    <br>
                </li>
                <br>
            </ul>
            <br>
            <br>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios';

const localhost = 'http://localhost:8081';
export default {
  components: {
  },
  data(){
    return{
      productos: [],
      selected: '',
      categorias: [
        {
          nombreCategoria: "Importado"
        },
        {
          nombreCategoria: "Nacional"
        }
      ],
      productos_filtrados: [],
      categoria_seleccionado: 0,
    }
  },
  methods: {
    getProductos(){
      const url = localhost + '/productos';
      axios.get(url).then((data) => {
        this.productos = data.data;
      });
    },
    seleccionarCategoria(){
      //Se seleccionan los productos correspondientes a esa categoría seleccionada

      this.productos_filtrados = [];

      for(let i = 0; i < this.productos.length; i++){
        if(this.productos[i].categoria == categoria.nombreCategoria){

          this.productos_filtrados.push(this.productos[i]);
        }
      }
    },
  },

  mounted() {
    this.getProductos();
  }
}
</script>
