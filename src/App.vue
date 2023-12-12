<template>
  <div class="wrapper">
    <form class="d-flex" role="search">
      <input v-model="searchProductInput" @input="searchProducts" placeholder="Search">
      <button class="btn btn-outline-success" type="submit">Search</button>
    </form>
    <div class="categories">
      <h3>Product Categories</h3>
      <select v-model="selectedCategory">
        <option value="">All Categories</option>
        <option v-for="category in uniqueCategories" :key="category" :value="category">{{ category }}</option>
      </select>
      <div v-if="selectedCategory">
        <h4>Products in {{ selectedCategory }}</h4>
        <div class="prodCard" v-for="product in productsInSelectedCategory" :key="product.id">
          <div class="card-header">
            <h3>{{ product.name }}</h3>
          </div>
          <div class="card-body">
            <img :src="product.img" :alt="product.name" loading="lazy">
            <p>R{{ product.amount }}</p>
          </div>
          <div class="card-footer">
            <a href="#" type="button">Add To Cart</a>
          </div>
        </div>
      </div>
      <div v-else>
        <h4>All Products</h4>
        <div class="prodCard" v-for="product in filteredProducts" :key="product.id">
          <div class="card-header">
            <h3>{{ product.name }}</h3>
          </div>
          <div class="card-body">
            <img :src="product.img" :alt="product.name" loading="lazy">
            <p>R{{ product.amount }}</p>
          </div>
          <div class="card-footer">
            <a href="#" type="button">Add To Cart</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      searchProductInput: '',
      selectedCategory: '',
      products: [
      {
          id: 1,
          name: "31-inch Skateboard",
          make: "Wood Street",
          amount: 599.99,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaCPFzVd0sNt146XUK7wiI551HPAJRdAR4rkoZBQy6SZrzS-_5BifBKbsuh7DXB0pwGq_T0Wf-xfUVkHHt5BCIfGlWE-=w1588-h1304",
        },
        {
          id: 2,
          name: "Reef Marble 34.74 Skatboard",
          make: "Wood Street",
          amount: 2199.0,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaBk0n_nORcBfFvcu7LWv0a18rpBjQSA1G2VUV8xVyWBzThUiF_8qWuUlm6DX1uNkgn2FudlOF8N41hNuJTOrmnayhNUBA=w1588-h1304",
        },
        {
          id: 3,
          name: "28 Inch Skateboard",
          make: "Wood Street",
          amount: 299.99,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaBe1MmEJGUrvuQCaqksP_i09FAmdBm402afKoVQqLq3Nqtn3TMg8zrXpKMCDewXTduHycVWQ70TE1EY4U15QqZV4mFw=w1588-h1304",
        },
        {
          id: 4,
          name: "Rad Skateboard",
          make: "Complete Cherry Blossom Black/Red (Size 7.75)",
          amount: 1199.0,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaC_vFwMR9ibII2xWjazYP4EBKNjoR4v_5yTll0j0P-dD2QuoFVfW17m8y3y_-DkyryVePJNcYMeEk8nst2go0KWTyG_wA=w1588-h1304",
        },
        {
          id: 5,
          name: "Magneto",
          make: "Mini Cruiser Skateboard",
          amount: 1318.09,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaBZA8Pbjnm3RdMlhzj8Jo7y46yqYNb2a_b7PT7FYUWyBDM7E4XAiAteGTcR6Rpi1OGKW1akhKGqrUzKqzZYjo4fmkqa=w1588-h1304 ",
        },
        {
          id: 6,
          name: "Rippa Skateboard",
          make: "Wood · Mini · Longboard",
          amount: 249.9,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaDdAdl1xK5l04OolCQmwpmyr5QwdOr3zIHMNpVPBelnLl2ERNQi0jykk_X95373TqaZD83kxr537KjF5-LBvaydufN32Q=w1588-h1304",
        },
        {
          id: 7,
          name: "Element Seal",
          make: "Skateboard Complete",
          amount: 1599.95,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaATXlNuoe1LEq_YciRkHiX-kPuHBEm_kSPSZZUD1OE61r68IkfSpKJx_uLxLb0BMwMoZmAziMQdr3eINRPj_aXbb90AQg=w1588-h1304",
        },
        {
          id: 8,
          name: "Skateboard Skull",
          make: "Black8Hole Modell 3103",
          amount: 339.19,
          img: "https://lh3.googleusercontent.com/u/0/drive-viewer/AK7aPaAE2NNl32zgVZalXtUzC7NtzskOcKhQmNAQUDuE-XEmu2GBPzcKBPZarstPh1htM33yftG_ZEzw2_ARhhODwCR4keCb9g=w1588-h1304",
        },
      ]
    }
  },
  computed: {
    uniqueCategories: function() {
      return [...new Set(this.products.map(product => product.make))];
    },
    filteredProducts: function() {
      const searchTerm = this.searchProductInput.toLowerCase();
      return this.products.filter(product =>
        product.name.toLowerCase().includes(searchTerm) ||
        product.make.toLowerCase().includes(searchTerm)
      );
    },
    productsInSelectedCategory: function() {
      if (this.selectedCategory) {
        return this.products.filter(product => product.make === this.selectedCategory);
      } else {
        return [];
      }
    }
  },
  methods: {
    searchProducts() {
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
