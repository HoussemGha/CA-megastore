<template>
    <div>
         <div class="bg-light py-3">
      <div class="container">
        <div class="row">
          <div class="col-md-12 mb-0"><a href="index.html">Acceuil</a> <span class="mx-2 mb-0">/</span> <strong class="text-black">Boutique</strong></div>
        </div>
      </div>
    </div>

    <div class="site-section">
      <div class="container">

        <div class="row mb-5">
          <div class="col-md-9 order-2">
           
            <div class="row">
              <div class="col-md-12 mb-5">

                <div class="d-flex">
             
                  <div class="btn-group">
                    <button type="button" class="btn text-white btn-sm" style="background-color:#ff0000" @click="getproducts()">Liste des Produits</button>
                    
                  </div>
                </div>
              </div>
            </div>
           
            <div class="row mb-5">
              <!-- -->
              <div class="col-sm-6 col-lg-4 mb-4" v-for="product in products" :key="product.title">
                  <nuxt-link :to="'/product/' + product.title">
                <div class="block-4 text-center border">
                  <figure class="block-4-image" style="height: 135px;">
                  <img :src="product.image" alt="Image placeholder" class="img-fluid" style="height: 154px;">
                  </figure>
                  <div class="block-4-text p-4">
                    <p class="mb-0" style="height: 54px;">{{product.title}}</p>
                    <h5 class="font-weight-bold" style="color:#ff3838;">{{product.price}}.00 € </h5>
                  </div>
                </div>

                </nuxt-link>
              </div>
            <!-- -->


            </div>
            <div class="row">
              <div class="col-md-12 text-center">
                <div class="site-block-27">
                  <ul>
                    <li><a href="#">&lt;</a></li>
                    <li class="active"><span>1</span></li>
                    <li><a href="#">2</a></li>
                    <li><a href="#">3</a></li>
                    <li><a href="#">4</a></li>
                    <li><a href="#">5</a></li>
                    <li><a href="#">&gt;</a></li>
                  </ul>
                </div>
              </div>
            </div>
          </div>

          <div class="col-md-3 order-1 mb-5 mb-md-0">
            <div class="border p-4 rounded mb-4">
              <h3 class="mb-3 h6 text-uppercase text-black d-block">Categories</h3>
              <ul class="list-unstyled mb-0">
                <li class="mb-1" ><a @click="filterProducts('category','BAGUES')" class="d-flex colorp" style="cursor:pointer"><span>VESTES</span></a></li>
                <li class="mb-1"><a  @click="filterProducts('category','BRACELETS')" class="d-flex colorp" style="cursor:pointer"><span>SURVETEMENTS</span></a></li>
                <li class="mb-1"><a @click="filterProducts('category','COLLIERS ET PENDENTIFS')" class="d-flex colorp" style="cursor:pointer"><span>MAILLOTS</span></a></li>
                <li class="mb-1"><a  @click="filterProducts('category','BOUCLES A OREILLES')" class="d-flex colorp " style="cursor:pointer"><span>ACCESOIRES</span> </a></li>

              </ul>
            </div>

            <div class="border p-4 rounded mb-4">
              <div class="mb-4">
                <h3 class="mb-3 h6 text-uppercase text-black d-block">Filter Par Prix</h3>
                 <range-slider
                    class="slider"
                    min="100"
                    max="5000"
                    step="10"
                    v-model="sliderValue"  @change="filterByPrice" >
                </range-slider>
                <p>{{sliderValue}}.00 € </p>
              </div>

              <div class="mb-4">
                <h3 class="mb-3 h6 text-uppercase text-black d-block">Couleurs</h3>
                <a class="d-flex color-item align-items-center" @click="filterProducts('color','OR BLANC')" style="cursor:pointer">
                  <span class=" color d-inline-block rounded-circle mr-2" style="background-color:#f5efef"></span> <span class="text-black">BLANC</span>
                </a>
                <a class="d-flex color-item align-items-center"  @click="filterProducts('color','OR JAUNE')"  style="cursor:pointer">
                  <span class="color d-inline-block rounded-circle mr-2" style="background-color:#ff0000"></span> <span class="text-black">ROUGE</span>
                </a>
                <a  class="d-flex color-item align-items-center" style="cursor:pointer" @click="filterProducts('color','OR ROSE')" >
                  <span class="color d-inline-block rounded-circle mr-2" style="background-color:#9c9c9c"></span> <span class="text-black">GRIS</span>
                </a>
                <a  class="d-flex color-item align-items-center" style="cursor:pointer" @click="filterProducts('color','PLATINE')" >
                  <span class="color d-inline-block rounded-circle mr-2" style="background-color:#000000"></span> <span class="text-black">NOIR</span>
                </a>
                
              </div>

              <div class="mb-4">
                <h3 class="mb-3 h6 text-uppercase text-black d-block">Taille</h3>
                <label for="s_sm" class="d-flex">
                  <input type="checkbox" id="s_sm" class="mr-2 mt-1"> <span class="text-black" @click="filterProducts('size','UN')">UNIQUE</span>
                </label>
                <label for="s_md" class="d-flex">
                  <input type="checkbox" id="s_md" class="mr-2 mt-1"> <span class="text-black">S</span>
                </label>
                <label for="s_lg" class="d-flex">
                  <input type="checkbox" id="s_lg" class="mr-2 mt-1"> <span class="text-black">M</span>
                </label>
                <label for="s_lg" class="d-flex">
                  <input type="checkbox" id="s_lg" class="mr-2 mt-1"> <span class="text-black">L</span>
                </label>
                <label for="s_lg" class="d-flex">
                  <input type="checkbox" id="s_lg" class="mr-2 mt-1"> <span class="text-black">XL</span>
                </label>
              </div>

              
            </div>
          </div>
        </div>

       
        
      </div>
    </div>
    </div>
</template>

<script>
import RangeSlider from 'vue-range-slider'
// you probably need to import built-in style
import 'vue-range-slider/dist/vue-range-slider.css'

export default {
data(){
  return{
      sliderValue: 100,
      products:[]
  }
},
components: {
  RangeSlider
},
created(){
  this.getproducts()
},
methods: {
   getproducts(){
       let files =  require.context('~/assets/content/product/', false, /\.json$/);
        this.products = files.keys().map(key => {
        let res = files(key);
        return res;
      });
   },
   
   filterByPrice() {
        this.getproducts()
        let  productFilters =[]
        this.products.forEach(element => {
          if(element.price<=this.sliderValue){
            productFilters.push(element)
          }
      })
      console.log(productFilters)
      this.products=productFilters
    },
    filterProducts(type,valeur){
     this.getproducts()
      let productFilters=[]    
      switch (type) {
        case 'category':
          this.products.forEach(element => {
            if(element.category==valeur){
              productFilters.push(element)
            }
         })
          break;
        case 'color':
            this.products.forEach(element => {
            if(element.color==valeur){
              productFilters.push(element)
            }
         })
           break;
        case 'size':
          this.products.forEach(element => {
            if(element.size==valeur){
              productFilters.push(element)
            }
          })
          break;
        default:
          console.log(`Sorry, we are out of.`);
      }
     
       this.products=productFilters

    }
    
  }
};
</script>

<style scoped>

.colorp{
  color: #7971ea;
}
.slider {
  /* overwrite slider styles */
  width: 200px;
}

</style>>
