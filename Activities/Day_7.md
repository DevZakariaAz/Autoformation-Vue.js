### **Day 7: Build a Final Project – Recipe Manager**

#### **Objective**

Create a fully functional **"Recipe Manager"** app that incorporates everything you've learned in the week: Vue Router, state management, Composition API, reusable components, form validation, and animations.

---

### **Activities**

#### **1. Project Setup**

- **Initialize the Project**:
  - Use Vue CLI or Vite to scaffold your app.
  - Install necessary dependencies:
    - **Vue Router** for navigation.
    - **Pinia or Vuex** for state management.
    - **VeeValidate** for form validation.
    - **Tailwind CSS** or **Vuetify** for styling.
  ```bash
  npm install vue-router pinia vee-validate tailwindcss
  ```
- **Create Project Structure**:
  - Organize folders (`components/`, `views/`, `store/`, `assets/`, etc.).

---

#### **2. Implement Core Features**

##### **2.1 Routing with Vue Router**

- Set up routes for key pages:
  - `/` – Home (list all recipes).
  - `/recipe/:id` – View detailed recipe.
  - `/add` – Add a new recipe.
  ```javascript
  const routes = [
    { path: "/", component: Home },
    { path: "/recipe/:id", component: RecipeDetails },
    { path: "/add", component: AddRecipe },
  ];
  ```

##### **2.2 State Management with Pinia or Vuex**

- Set up a global store to manage:
  - Recipes (CRUD operations).
  - Favorites list.
  ```javascript
  export const useRecipeStore = defineStore("recipeStore", {
    state: () => ({
      recipes: [],
      favorites: [],
    }),
    actions: {
      addRecipe(recipe) {
        this.recipes.push(recipe);
      },
      toggleFavorite(id) {
        const recipe = this.recipes.find((r) => r.id === id);
        recipe.isFavorite = !recipe.isFavorite;
      },
    },
  });
  ```

##### **2.3 Composition API for Logic**

- Use `ref` and `reactive` for local state in components.
- Example: Manage form inputs in `AddRecipe.vue`.

  ```javascript
  import { ref } from "vue";

  const title = ref("");
  const ingredients = ref([]);
  const steps = ref("");
  ```

##### **2.4 Dynamic Recipe Details**

- Fetch recipe details using the ID from the URL.

  ```javascript
  import { useRoute } from "vue-router";

  const route = useRoute();
  const recipeId = route.params.id;
  const recipe = computed(() => store.recipes.find((r) => r.id === recipeId));
  ```

---

#### **3. Add Advanced Features**

##### **3.1 Form Validation (VeeValidate)**

- Validate the recipe form to ensure all fields are filled.
- Example:
  ```html
  <form @submit.prevent="submitForm">
    <input v-model="title" required />
    <span v-if="errors.title">Title is required</span>
  </form>
  ```

##### **3.2 Animations and Transitions**

- Add transitions for navigating between pages or showing modals.
  ```html
  <transition name="fade">
    <div v-if="showModal">Modal Content</div>
  </transition>
  ```
  ```css
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.5s;
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
  ```

##### **3.3 Responsive Design**

- Use CSS frameworks like **Tailwind CSS** to create a polished, mobile-friendly UI.
  ```html
  <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
    <!-- Recipe cards -->
  </div>
  ```

---

#### **4. Final Touches**

- **Testing**:

  - Test all routes and functionalities for bugs.
  - Handle edge cases (e.g., invalid recipe IDs).

- **Deployment**:
  - Deploy the app using platforms like Netlify, Vercel, or GitHub Pages.

---

### **Outcome**

By the end of the day, you will have a fully functional **Recipe Manager** app that demonstrates your mastery of Vue.js!
