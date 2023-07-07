<template>
  <div id="app">
    <header>
      <nav>
        <ul>
          <li v-for="link in links" :key="link.path">
            <router-link :to="link.path" class="nav-link" :style="{ backgroundColor: link.bgColor, color: link.textColor }" @click="animateButton">{{ link.label }}</router-link>
          </li>
        </ul>
      </nav>
    </header>
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      links: [
        { path: '/', label: 'Weather', bgColor: '#007bff', textColor: '#fff' },
        { path: '/location', label: 'Location', bgColor: '#28a745', textColor: '#fff' },
        { path: '/stopwatch', label: 'Stopwatch', bgColor: '#dc3545', textColor: '#fff' },
        { path: '/tictactoe', label: 'Tic Tac Toe', bgColor: '#ffc107', textColor: '#333' },
        { path: '/photo', label: 'Photo', bgColor: '#17a2b8', textColor: '#fff' }
      ]
    };
  },
  methods: {
    animateButton(event) {
      event.target.classList.add('button-animation');
      setTimeout(() => {
        event.target.classList.remove('button-animation');
      }, 300);
    }
  }
};
</script>

<style>
#app {
  text-align: center;
  background: #f2f2f2;
}

header {
  background: #10d7f1;
  padding: 20px;
}

nav ul {
  list-style: none;
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: flex-end;
}

nav li {
  margin-left: 10px;
}

.nav-link {
  color: inherit;
  text-decoration: none;
  padding: 10px;
  border-radius: 5px;
  border: none;
  transition: background-color 0.3s;
}

.button-animation {
  animation-name: button-click;
  animation-duration: 0.3s;
  animation-timing-function: ease-in-out;
}

@keyframes button-click {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(0.9);
  }
  100% {
    transform: scale(1);
  }
}

router-link-active {
  background-color: rgba(0, 123, 255, 0.2);
}
</style>
