<script>
export default {
  props: ["mensajes"],
};
</script>

<template>
  <div class="chat">
    <div
      v-for="(mensaje, i) in mensajes" :key="i" :class="{ izquierda: mensaje.persona === 'persona1', derecha: mensaje.persona === 'persona2'}">
      <span>{{ mensaje.nombre }}</span>
      <p class="mensaje" :style="{ backgroundColor: mensaje.input }" :class="{ colorTexto: mensaje.input === '#000' }">
        {{ mensaje.textarea }}
      </p>
    </div>
  </div>
</template>

<style>
.chat {
  border: 1px solid grey;
  width: 500px;
  height: 385px;
  margin: 0 1rem 0;
  padding: 1rem;
  overflow: scroll;
  background-image: url("https://preview.redd.it/qwd83nc4xxf41.jpg?auto=webp&s=172adf428061ec1b71c0d43b7ba870f85d46a816");
  background-size: cover;
}

.derecha {
  text-align: right;
}

.izquierda {
  text-align: left;
}

span {
  font-size: 14px;
  display: block;
}

.mensaje {
  display: inline-block;
  border-radius: 20px;
  padding: 9px;
  box-shadow: 7px 10px 22px -5px rgba(161, 161, 161, 1);
  word-wrap: break-word;
  max-width: 90%;
  text-align: center;
}

.colorTexto {
  color: #fff;
}
</style>
