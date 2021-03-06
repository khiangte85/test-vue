<script setup>
import { ref } from 'vue'

const excludeKeys = ['price', 'id']
const inputSize = ref(1)
const outputArray = ref([])
const inputObject = {
  'Performer Orchestra': 'Chicago Symphony Orchestra',
  price: 1,
  quantity: 1,
  id: 'A7GNyD',
  'Fidelity Level': 'Low-Fidelity',
  Instrument: 'Acoustic Guitar',
}

const generate = () => {
  let inputArray = Array.from({ length: inputSize.value }, () => inputObject)
  outputArray.value = inputArray.map((item, i) => {
    let skus = []
    
    Object.keys(item).forEach((key, j) => {
      if (!excludeKeys.includes(key)) {
        skus.push(key.slice(0, 2).toLowerCase())
      }

      if (j === Object.keys(item).length - 1) {
        skus.push(i < 9 ? `0${i + 1}` : i + 1)
      }
    })

    return {
      ...item,
      sku: skus.join('_'),
    }
  })
}
</script>

<template>
  <div>
    <h3>Input</h3>
    <pre
      :style="{
        backgroundColor: '#cccccc',
        padding: '20px',
      }"
      >{{ inputObject }}</pre
    >
    <div>
      Input array size:
      <input type="number" min="1"  v-model="inputSize" />
      <button type="button" @click="generate">Generate Output</button>
    </div>
  </div>
  <div :style="{ marginLeft: '20px' }">
    <h3>Output</h3>
    <pre
      :style="{
        backgroundColor: '#cccccc',
        padding: '20px',
        maxHeight: '500px',
        overflow: 'scroll',
      }"
      >{{ outputArray }}</pre
    >
  </div>
</template>

<style>
@import './assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;

  font-weight: normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
