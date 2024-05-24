<template>
  <q-layout view="hHh lpR fFf">
    <!-- Navbar -->
    <q-header elevated class="bg-primary text-white">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />
        <q-toolbar-title>
          Toko Gihara
        </q-toolbar-title>
        <q-btn dense flat round icon="shopping_cart" @click="goToCart" />
      </q-toolbar>
    </q-header>

    <!-- Left Drawer -->
    <q-drawer v-model="leftDrawerOpen" side="left" width="200">
      <q-list>
        <q-item clickable v-ripple>
          <q-item-section>
            Home
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            Products
          </q-item-section>
        </q-item>
        <q-item clickable v-ripple>
          <q-item-section>
            About Us
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <!-- Main Content -->
    <q-page-container>
      <q-page padding class="q-pa-md">
        <!-- Carousel -->
        <q-carousel
          v-model="slide"
          arrows
          infinite
          animated
          control-color="black"
          swipeable
          transition-prev="slide-right"
          transition-next="slide-left"
          height="550px"
          class="bg-dark text-white shadow-2 rounded-borders"
        >
          <q-carousel-slide v-for="(image, index) in carouselImages" :key="index" :name="index" :img-src="image">
          </q-carousel-slide>
        </q-carousel>

        <!-- Cards -->
        <div class="q-mt-xl row justify-center">
          <q-card v-for="product in products" :key="product.name" class="my-card q-mb-xl q-pa-md col-xs-12 col-sm-6 col-md-4 col-lg-3">
            <q-img :src="product.image" :alt="product.name" class="my-card-img">
              <q-badge color="red" floating>{{ product.discount }}Flash Sale</q-badge>
            </q-img>
            <q-card-section>
              <div class="text-h6 text-center">{{ product.name }}</div>
              <div class="text-subtitle1 text-center">{{ product.price }}</div>
            </q-card-section>
            <q-card-actions align="center">
              <q-btn flat label="Add to Cart" color="primary" @click="addToCart(product)" />
            </q-card-actions>
          </q-card>
        </div>
      </q-page>
    </q-page-container>

    <!-- Footer -->
    <q-footer class="bg-blue-8 text-white">
      <q-toolbar>
        <q-toolbar-title>
          &copy; Toko Gihara
        </q-toolbar-title>
        <div>
          <q-btn flat round icon="facebook" />
          <q-btn flat round icon="twitter" />
          <q-btn flat round icon="instagram" />
        </div>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const slide = ref(0);
    const carouselImages = [
      'https://th.bing.com/th/id/OIP.4Xys25CzrknwT15IQzz0dAHaHa?w=207&h=207&c=7&r=0&o=5&dpr=1.3&pid=1.7',  // Ganti dengan URL gambar kita
      'https://th.bing.com/th/id/OIP.g6j4DVM6W0hE4B7MYxRZLwHaGR?w=220&h=187&c=7&r=0&o=5&dpr=1.3&pid=1.7',
      'https://cdn1.productnation.co/stg/sites/5/5c99ab9c32066.jpeg'
    ];
    const products = [
      { name: 'Baju Kaos  1', price: 'Rp. 100K', image: 'https://th.bing.com/th/id/OIP.0J-HAj7uzUfE-_dVV_reBQAAAA?w=199&h=199&c=7&r=0&o=5&dpr=1.3&pid=1.7'},  // Ganti dengan URL gambar kita
      { name: 'Baju Kaos 2', price: 'Rp. 200K', image: 'https://th.bing.com/th/id/OIP.Fndm_SktZ9bIAjj4cmEhVgHaHa?w=185&h=186&c=7&r=0&o=5&dpr=1.3&pid=1.7'},
      { name: 'Baju Kaos 3', price: 'Rp. 250K', image: 'https://th.bing.com/th/id/OIP.j7UlAXVytwTtfjuv_69vZgHaHa?w=163&h=180&c=7&r=0&o=5&dpr=1.3&pid=1.7'},
      { name: 'Diamond', price: 'Rp. 20k-250K', image: 'https://th.bing.com/th/id/OIP.Svz9PVP96vvqcGzdhoZipQHaHc?w=143&h=180&c=7&r=0&o=5&dpr=1.3&pid=1.7'},
      { name: 'Baju  Kaos 5', price: 'Rp. 300K', image: 'https://th.bing.com/th/id/OIP.ADoNtmgonhpLsrC3pkY-wgHaHa?w=206&h=206&c=7&r=0&o=5&dpr=1.3&pid=1.7'}
    ];
    const cart = ref([]);

    const toggleLeftDrawer = () => {
      leftDrawerOpen.value = !leftDrawerOpen.value;
    };

    const goToCart = () => {
      console.log('Navigating to cart...');
      // Logic untuk membuka halaman keranjang atau menampilkan keranjang
    };

    const addToCart = (product) => {
      cart.value.push(product);
      console.log(`${product.name} telah ditambahkan ke keranjang`);
    };

    return {
      leftDrawerOpen,
      toggleLeftDrawer,
      slide,
      carouselImages,
      products,
      addToCart,
      goToCart
    };
  }
};
</script>

<style>
.my-card {
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
  border-radius: 10px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
}
.my-card-img {
  border-radius: 10px 10px 0 0;
  height: 200px;
}
.rounded-borders {
  border-radius: 10px;
}
.q-footer {
  border-top: 1px solid #7a0085;
}
</style>
