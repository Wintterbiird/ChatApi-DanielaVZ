<script>
import axios from "axios";
import Chat from "./components/Chat.vue";

export default {
  components: {
    Chat,
  },
  data() {
    return {
      persona1: {
        imagen: {},
        nombre: "",
        apellido: "",
        input: "#000",
        textarea: "",
      },
      persona2: {
        imagen: {},
        nombre: "",
        apellido: "",
        input: "#000",
        textarea: "",
      },
      mensajes: [],
    };
  },
  mounted() {
    this.obtenerPersonas();
  },
  methods: {
    async obtenerPersonas() {
      const url = "https://randomuser.me/api/?results=2";
      const { data } = await axios.get(url);
        this.persona1.imagen = data.results[0].picture.large;
        this.persona1.nombre = data.results[0].name.first;
        this.persona1.apellido = data.results[0].name.last;

        this.persona2.imagen = data.results[1].picture.large;
        this.persona2.nombre = data.results[1].name.first;
        this.persona2.apellido = data.results[1].name.last;
  },
    enviarMsje(persona) {
      this.mensajes.push({
        nombre: this[persona].nombre,
        textarea: this[persona].textarea,
        input: this[persona].input,
        persona,
      });
    },
  },
};
</script>

<template>
  <div id="App">
    <div class="persona1">
      <img :src="persona1.imagen" />
      <p>{{ persona1.nombre }} {{ persona1.apellido }}</p>
      <input v-model="persona1.input" type="color" />
      <textarea @keyup.enter="enviarMsje('persona1')" v-model="persona1.textarea"  rows="10" cols="50"></textarea>
      <button @click="enviarMsje('persona1')">Enviar</button>
    </div>

    <Chat :mensajes="mensajes" />

    <div class="persona2">
      <img :src="persona2.imagen" />
      <p>{{ persona2.nombre }} {{ persona2.apellido }}</p>
      <input v-model="persona2.input" type="color"/>
      <textarea @keyup.enter="enviarMsje('persona2')" v-model="persona2.textarea" name="textarea" rows="10" cols="50"> </textarea>
      <button @click="enviarMsje('persona2')">Enviar</button>
    </div>
  </div>
</template>

<style scoped>
#App {
  display: flex;
  justify-content: center;
  align-items: flex-start;
}
.persona1 {
  width: 150px;
  display: flex;
  flex-direction: column;
  height: 418px;
}

.persona2 {
  width: 150px;
  display: flex;
  flex-direction: column;
  height: 418px;
}

input {
  width: 100%;
}

button {
  width: 100%;
  background-color: #e3e3e3;
  color: #000;
  padding: 3px;
}

.left {
  align-items: flex-start;
}

.right {
  align-items: flex-end;
}
</style>
