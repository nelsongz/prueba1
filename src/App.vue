<script setup>
  import {ref, computed} from 'vue'

  const name = 'Vue Dinamico'
  const styleColor = 'color: blue'
  const arrayColores = ["blue","red","yellow"]
  const activo = true
  const arrayFrutas = ["🍎", "🍌", "🍉", "🍓", "🍒"]
  const arrayObjFrutas = [
        {
            name: "Manzanas",
            price: "$1.00",
            description: "Una manzana",
            stock: 0
        },
        {
            name: "Pera",
            price: "$2.00",
            description: "Una pera",
            stock: 5
        },
        {
            name: "Naranja",
            price: "$3.00",
            description: "Una naranja",
            stock: 12
        },
    ]
  const objetoFrutas = 
        {
            name: "Manzana",
            price: "$1.00",
            description: "Una manzana",
        }

  let contador = ref(0)
  // metodos
  const handleClick = (mensaje) => {
    console.log(mensaje)
  }
  const increment = () => {
    contador.value ++
  }
  const decrement = () => {
    contador.value --
  }
  const resetear = () => {
    contador.value = 0
  }

  const classCounter = computed(() => {
    if (contador.value === 0) {
      return "zero"
    }
    if (contador.value > 0) {
      return "positive"
    }
    if (contador.value < 0) {
      return "negative"
    }
  })

  let favoritos = ref([])
  const add = () => {
    favoritos.value.push(contador.value)
  }
  const repetido = computed (() => {
    return favoritos.value.includes(contador.value)
  })
</script>

<template>
  <div class="container">
      <h1>Hola {{ name }}</h1>
      <h1>Hola {{ name.toUpperCase() }}</h1>
      <h2 v-bind:style="styleColor">Soy azul</h2>
      <h2 :style="styleColor">Soy el mismo azul</h2>
      <h2 :style="`color: ${arrayColores[2]}`">Ahora soy amarillo</h2>
      <h3>
        {{ activo ? 'Estoy activo' : 'Estoy inactivo'}}
      </h3>
      <h3 v-if="activo">Estoy activo</h3>
      <h3 v-else>Estoy inactivo</h3>
      <h3 v-show="activo">Con v-show solo se oculta con style</h3>
      <p>{{ arrayFrutas}}</p>
      <ul>
        <li v-for="(fruta,index) in arrayFrutas" :key="index">
          {{index}} - {{fruta}}
        </li>
      </ul>
      <h4>Combinar v-if con v-for</h4>
      <ul>
        <template v-for="item in arrayObjFrutas" :key="item.name">
          <li v-if="item.stock > 0">{{ item.name }} - {{ item.price }} - {{ item.stock }}</li>
        </template>
      </ul>

      <p>{{ arrayObjFrutas}}</p>
      <ul>
        <li v-for="(fruta,name) in arrayObjFrutas" :key="name">
          {{name}} - {{fruta.name}} - {{fruta.price}} - {{fruta.description}}
        </li>
      </ul>
      <p>{{ objetoFrutas}}</p>
      <ul>
        <li v-for="(value, propiedad, index) in objetoFrutas" :key="value">
            {{ index }} - {{ propiedad }} : {{ value }}
        </li>
      </ul>

      <button v-on:click.right.prevent="handleClick('texto Right')">Activame right</button>
      <button @click.left="handleClick('texto Left')">Activame left</button>
      <button @click.middle="handleClick('texto Middle')">Activame middle</button>
      <p></p>
      <p></p>
      <h2 :class="classCounter">Contador = {{ contador }}</h2>
      <div class="btn-group" role="group">
        <button @click="increment()" class="btn btn-primary">Aumentar contador</button>
        <button @click="decrement()" class="btn btn-success">Disminuir contador</button>
        <button @click="resetear()" class="btn btn-warning">Resetear contador</button>
        <button @click="add" :disabled="repetido" class="btn btn-info">Add</button>
      </div>
      <ul class="list-group" mt-7>
        <li class="list-group-item" v-for="(favorito, index) in favoritos" :key="index">
        {{ favorito}}
        </li>
      </ul>
  </div>
</template>

<style>
  h1 {
    color: red;
  }
  .positive {
    color: green;
  }
  .negative {
    color: red;
  }
  .zero {
    color: peru;
  }
</style>