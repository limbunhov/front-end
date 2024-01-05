<template>
    <section>
      <div v-if="isFavorite && !loading" class="fav_board">
        <div class="fav_cart" v-for="favorite in favorites" :key="favorite._id">
          <div class="fav_image">
            <img :src="favorite.product.image" :alt="favorite.product.title.t"/>
          </div>
          <div class="fav_detail">
            <div style="width: 40rem;">
              <h1>{{ favorite.product.name }}</h1>
              <p>{{ favorite.product.title.t1 }}</p>
              <p>{{ favorite.product.title.t2 }}</p>
              <p>{{ favorite.product.title.t3 }}</p>
              <p>{{ favorite.product.title.t4 }}</p>
              <!-- Add other product details here -->
            </div>
            <span>${{ favorite.product.price }}</span>
            <div class="button">
              <button @click="removeFromFavorites(favorite.product._id)" type="button" class="btn bg-danger"
                      style="height: 3rem; margin-right: 5rem; width: 7rem;">
                Remove
              </button>
            </div>
          </div>
        </div>
      </div>
      <div v-else class="not_add_cart m-3">
        <p>Sorry!! Please add to favorites.</p>
      </div>
    </section>
  </template>
  
  <script>
  import axios from 'axios';
  
  export default {
    data() {
        return {
            favorites: [],
            isFavorite: true,
            loading: false,
        };
    },
    created() {
      this.fetchFavorites();
    },
    methods: {
      async fetchFavorites() {
        try {
          const userId = localStorage.getItem('userId');
          console.log(userId);
  
          const response = await axios.get(`http://localhost:3000/favorites/${userId}`);
          this.favorites = response.data;
  
          console.error(response.data);
        } catch (error) {
          console.error('Error fetching favorites:', error);
        }
      },
      async removeFromFavorites(productId) {
        try {
            const token = localStorage.getItem('token');
            const userId = localStorage.getItem('userId');

            if (!token || !userId) {
            console.error('Token or userId not found.');
            return;
            }

            console.log(userId, productId);

            await axios.delete(`http://localhost:3000/favorites/${userId}/${productId}`);

            // Send a request to your server to remove the product from favorites
            // const response = await axios.delete(`http://localhost:3000/remove/favorites`, {
            //     data: {
            //         userId: userId,
            //         productId: productId,
            //     },
            // });


            this.favorites = this.favorites.filter(product => product.product._id !== productId);
            this.isFavorite = this.favorites.length > 0;
            // console.error('Failed to remove from favorites:', response.data.error);
        } catch (error) {
            console.error('Error removing from favorites:', error);
        }
        }

    },
  };
  </script>
  