<template>
  <main class="product-detail-container">
    <!-- Spinner Container -->
    <div v-if="loading" class="spinner-overlay">
      <div class="spinner"></div>
    </div>

    <!-- Product Details -->
    <div v-else-if="error" class="text-red-500">Error: {{ error }}</div>
    <div v-else-if="product" class="product-detail">
      <img :src="product.image" :alt="product.title" class="product-image" />
      <h1 class="product-title">{{ product.title }}</h1>
      <p class="product-description">{{ product.description }}</p>
      <p class="product-price">${{ product.price }}</p>
      <p class="product-category">{{ product.category }}</p>
      <p class="product-rating">Rating: {{ product.rating.rate }}</p>
      <p class="product-reviews">Number of Reviews: {{ product.rating.count }}</p>
    </div>
    <router-link to="/" class="back-link">Back to products</router-link>
  </main>
</template>

<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

export default {
  name: "ProductDetail",
  setup() {
    const route = useRoute();
    const id = route.params.id; // Get the product ID from the route parameters

    const product = ref(null);
    const loading = ref(true);
    const error = ref(null);

    const fetchProduct = async (id) => {
      try {
        const response = await fetch(`https://fakestoreapi.com/products/${id}`);
        if (!response.ok) {
          throw new Error(
            "Data fetching failed, please check your network connection."
          );
        }
        const data = await response.json();
        product.value = data;
      } catch (err) {
        error.value = err.message;
      } finally {
        loading.value = false;
      }
    };

    onMounted(() => {
      fetchProduct(id);
    });

    return {
      product,
      loading,
      error,
    };
  },
};
</script>

<style scoped>
.product-detail-container {
  max-width: 500px;
  margin: 20px auto;
  padding: 20px;
  background-color: white;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1); /* Box shadow */
  text-align: center;
  position: relative; /* Ensure this container doesn't overlap the fixed button */
}

.product-detail img {
  max-width: 100%;
  height: auto;
  border-radius: 8px;
}

.product-title {
  font-size: 1.5rem;
  font-weight: bold;
  margin-top: 15px;
}

.product-description {
  margin-top: 10px;
  color: #555;
}

.product-price {
  font-size: 1.2rem;
  color: #333;
  margin-top: 10px;
}

.product-category,
.product-rating,
.product-reviews {
  color: #777;
  margin-top: 5px;
}

.back-link {
  position: fixed;
  bottom: 20px;
  left: 20px;
  background-color: #007bff;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  text-decoration: none;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  transition: background-color 0.2s, box-shadow 0.2s;
}

.back-link:hover {
  background-color: #0056b3;
  box-shadow: 0 6px 8px rgba(0, 0, 0, 0.2);
}

/* Spinner Styles */
.spinner-overlay {
  position: fixed; /* Fixes the spinner overlay over the whole screen */
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(255, 255, 255, 0.8); /* Light background with some transparency */
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999; /* Ensures spinner is above all content */
}

.spinner {
  width: 50px;
  height: 50px;
  border: 6px solid #ddd;
  border-top: 6px solid #007bff; /* Blue top border */
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
