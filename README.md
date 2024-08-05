# Product Store

A modern product store application built with Vue.js, featuring a responsive layout, product listing, and detailed product views. This project uses Vue Router for navigation and Tailwind CSS for styling.

## Features

- **Product Listing**: Display products in a grid layout with sorting, searching, and filtering options.
- **Product Details**: View detailed information about each product including description, price, and reviews.
- **Responsive Design**: Adapts to different screen sizes with a sticky header and mobile-friendly menu.
- **Dynamic Routing**: Navigate between different product views using Vue Router.

## Project Structure

- **`src/`**: Contains the source code for the application.
  - **`components/`**: Vue components used in the application.
    - **`Header.vue`**: Header component with navigation.
    - **`ProductCard.vue`**: Displays individual product cards.
    - **`ProductDetails.vue`**: Shows detailed information about a selected product.
    - **`ProductList.vue`**: Lists all products with filtering and sorting options.
  - **`App.vue`**: Main application component, integrates header and router view.
  - **`main.js`**: Entry point of the application, sets up Vue and Vue Router.

## Installation

1. **Clone the Repository**:

   ```bash
   git clone https://github.com/your-username/product-store.git
