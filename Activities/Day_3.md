### **Day 3: Vue Router**

**Objective**: Explore routing and navigation between pages.

---

#### **Activities**

1. **Install and Configure Vue Router**

   - Install Vue Router in your project:
     ```bash
     npm install vue-router
     ```
   - Create a `router.js` file to define routes:

     ```javascript
     import { createRouter, createWebHistory } from "vue-router";
     import Home from "./views/Home.vue";
     import About from "./views/About.vue";

     const routes = [
       { path: "/", component: Home },
       { path: "/about", component: About },
     ];

     const router = createRouter({
       history: createWebHistory(),
       routes,
     });

     export default router;
     ```

   - Register the router in your main `main.js` file:

     ```javascript
     import { createApp } from "vue";
     import App from "./App.vue";
     import router from "./router";

     createApp(App).use(router).mount("#app");
     ```

---

2. **Learn Routing Basics**
   - Read the [Vue Router Basics](https://router.vuejs.org/guide/) guide.
   - Understand key concepts:
     - **Routes**: Map URLs to components.
     - **`<router-view>`**: Render the current route's component.
     - **`<router-link>`**: Navigate between pages.
   - Example in `App.vue`:
     ```html
     <template>
       <div>
         <nav>
           <router-link to="/">Home</router-link>
           <router-link to="/about">About</router-link>
         </nav>
         <router-view></router-view>
       </div>
     </template>
     ```

---

3. **Explore Dynamic Routing**
   - Learn how to pass parameters to routes:
     ```javascript
     const routes = [{ path: "/post/:id", component: Post }];
     ```
   - Access route parameters in the component:
     ```javascript
     export default {
       setup(props, { route }) {
         const postId = route.params.id;
         console.log(postId);
       },
     };
     ```

---

4. **Learn Navigation Guards**

   - Add guards to protect routes or trigger actions before navigation:

     ```javascript
     const router = createRouter({
       history: createWebHistory(),
       routes,
     });

     router.beforeEach((to, from, next) => {
       if (to.path === "/protected" && !isAuthenticated()) {
         next("/");
       } else {
         next();
       }
     });
     ```

---

5. **Build a Multi-Page App**
   - Create a "Blog App" with the following pages:
     - **Home**: Display a welcome message.
     - **Posts**: List all blog posts with links to individual post pages.
     - **Post Details**: Display details for a specific post using dynamic routing (`/post/:id`).
     - **About**: Provide information about the app.
   - Directory structure:
     ```plaintext
     src/
     ├── views/
     │   ├── Home.vue
     │   ├── Posts.vue
     │   ├── Post.vue
     │   └── About.vue
     └── router.js
     ```

---

6. **Optional Challenge**
   - Add a 404 page for unmatched routes using the `path: '*'` route.
   - Add breadcrumbs for navigation to show the current route hierarchy.

---

#### **Estimated Time**: 3–4 hours
