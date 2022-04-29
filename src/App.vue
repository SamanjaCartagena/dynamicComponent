<template>
  <div>
<router-link to="/">Home</router-link>
  <button @click="createComponent">Create Component</button>

  <router-view></router-view>
  </div>
</template>

<script>
import { getCurrentInstance } from "vue";
import router from './router'
export default {
  name: "App",
  setup() {
    const app = getCurrentInstance().appContext.app;
   console.log(app)
    const createComponent = () => {
      // Check if the component has been alreadey registered
      if (!app.component("NewComponent")) {
        app.component("NewComponent", {
          name: "NewComponent",
          template: `<div id="new">This is a new component</div>`
        });
      }

      const newComponent = app.component("NewComponent");
      // Adding a new route to the new component
     
    router.addRoute({ path: "/new", component: newComponent });

     router.push("/new");
    };
    return {
      createComponent,
    };
  },
};
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
