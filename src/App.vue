<template>
  <div id="app">
    <nav>
      <router-link to="/">
        <div class="navigation__logo">
          Twooter
        </div>
      </router-link>
      <div class="navigation__user" v-if="user">
        {{ user.username }}
      </div>
    </nav>

    <router-view />
  </div>
</template>

<script>
import { useStore } from 'vuex'
import { computed } from 'vue'

export default {
  name: 'App',
  setup() {
    const store = useStore()
    const user = computed(() => store.state.User.user)

    return {
      user
    }
  }
}
</script>

<style lang="scss">
  body {
    margin: 0;
  
    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      color: #2c3e50;
      min-height: 100vh;
      background-color: #f3f5fa;

      nav {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 10px 5%;
        background-color: deeppink;
        color: white;

        a {
          text-decoration: none;
          color: inherit;
        }

        .navigation-logo {
          font-weight: bold;
          font-size: 24px;
        }
      }
    }
  }
</style>
