<template>
  <header class="sticky top-0 bg-gray-500 z-50">
    <nav class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4">
      <router-link to="/" class="flex items-center space-x-3 rtl:space-x-reverse">
        <img src="../assets/online-shop.png" class="h-8" alt="SwiftCart Logo" />
        <span class="text-2xl font-semibold text-white">SwiftCart</span>
      </router-link>
      <!-- Menu toggle button for mobile view -->
      <button @click="isOpen = !isOpen" type="button" class="text-white md:hidden">
        <svg class="w-5 h-5" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 17 14">
          <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M1 1h15M1 7h15M1 13h15" />
        </svg>
      </button>
      <div :class="{ 'block': isOpen, 'hidden': !isOpen }" class="w-full md:block md:w-auto">
        <ul class="flex flex-col md:flex-row md:space-x-8">
          <li class="relative">
            <router-link to="/wishlist" class="text-white md:hover:text-blue-700 flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-6 w-6 stroke-white cursor-pointer">
                <path stroke-linecap="round" stroke-linejoin="round" d="M3.172 4.172a4 4 0 015.656 0L12 7.343l3.172-3.171a4 4 0 115.656 5.656L12 19.828l-8.828-8.828a4 4 0 010-5.656z" />
              </svg>
              <span v-if="wishlistCount > 0" class="absolute top-0 right-0 bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">{{ wishlistCount }}</span>
            </router-link>
          </li>
          <li class="relative">
            <router-link to="/cart" class="text-white md:hover:text-blue-700 flex items-center">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="h-6 w-6 stroke-white cursor-pointer">
                <path stroke-linecap="round" stroke-linejoin="round" d="M2.25 3h1.386c.51 0 .955.343 1.087.835l.383 1.437M7.5 14.25a3 3 0 00-3 3h15.75m-12.75-3h11.218c1.121-2.3 2.1-4.684 2.924-7.138a60.114 60.114 0 00-16.536-1.84M7.5 14.25L5.106 5.272M6 20.25a.75.75 0 11-1.5 0 .75.75 0 011.5 0zm12.75 0a.75.75 0 11-1.5 0 .75.75 0 011.5 0z" />
              </svg>
              <span v-if="cartCount > 0" class="absolute top-0 right-0 bg-red-500 text-white text-xs rounded-full h-5 w-5 flex items-center justify-center">{{ cartCount }}</span>
            </router-link>
          </li>
          <li>
            <router-link to="/comparison" class="text-white md:hover:text-blue-700">
              Comparison
            </router-link>
          </li>
          <li>
            <!-- Dark Mode Toggle Button -->
            <button @click="$emit('toggle-dark-mode')" class="text-white">
              {{ isDarkMode ? 'Light Mode' : 'Dark Mode' }}
            </button>
          </li>
          <!-- Conditional rendering of Login/Logout button based on authentication state -->
          <li v-if="!isAuthenticated">
            <button @click="$emit('toggle-login')" class="text-white">
              Login
            </button>
          </li>
          <li v-else>
            <button @click="logout" class="text-white">
              Logout
            </button>
          </li>
        </ul>
      </div>
    </nav>
  </header>
</template>

<script>
import { mapGetters } from 'vuex';

export default {
  name: 'Header',
  data() {
    return {
      isOpen: false, 
    };
  },
  props: {
    isAuthenticated: {
      type: Boolean,
      required: true
    },
    isDarkMode: {
      type: Boolean,
      required: true
    }
  },
  computed: {
    ...mapGetters({
      cartCount: 'cartItemCount', 
      wishlistCount: 'wishlist.length'
    }),
  },
  methods: {
    logout() {
      this.$emit('logout');
    },
  }
};
</script>

<style scoped>
/* Add any styles specific to your header component */
</style>
