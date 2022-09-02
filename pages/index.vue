<template>
  <div>
    <div class="container">
      <div class="row">
          <div class="col-lg-12 text-center mt-4">
              <h1 class="page-title">Products</h1>              
          </div> 
          <div class="col-lg-12 mt-5">
              <table class="table table-striped">
                  <thead>
                    <tr>
                      <th scope="col">ID</th>                   
                      <th scope="col">Name</th>
                      <!-- <th scope="col">Image</th> -->
                      <th scope="col">Price</th>
                      <th scope="col">Status</th>
                      
                    </tr>
                  </thead>
                  <tbody>
                       <tr v-for="product in products">
                           <td scope="row">{{ product.id }}</td>
                           <td>{{ product.name }}</td>
                           <!-- <td><img src="{{ config('images.access_path')}}/{{ product.images.name }}" alt="" width="150px"></td> -->
                           <td>{{ product.price }}</td>
                           <td>
                              <span v-if="product.status == 0" class="badge rounded-pill text-bg-danger">Unavailable</span>
                              <span v-else class="badge rounded-pill text-bg-success">Available</span>
                            </td>
                          

                       </tr>               
                  </tbody>
                </table>
          </div>         
      </div>
     </div> 
  </div>
</template>

<script>
import { METHODS } from 'http';

export default {
  name: 'home',
  layout: 'dashboard',
  data(){
    return{
      products:[],
    }    
  },

  methods:  {
  getProducts(){
  this.$axios.get('/api/product').then(Response => {  
    this.products = Response.data;
    console.log(this.products);
  });
  
  }
  },
  

  mounted(){
    this.getProducts();
  },
}



</script>

<style>
  .page-title{
    padding-top: 5vh;
    font-size: 5rem;
  }
</style>