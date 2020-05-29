<template>
  <v-container grid-list-lg>
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <v-card>
          <v-img src="https://images.template.net/wp-content/uploads/2019/03/Featured-Image18.jpg" width="600" height="286"></v-img>
          <v-card-title><h2>Pizza Special</h2></v-card-title>
          <v-card-text>La mejor de nuestra casa pruebala ordena ahora</v-card-text>
          <v-card-actions><v-btn rounded color="info">ordenar</v-btn></v-card-actions>
        </v-card>
      </v-flex>
      <v-flex xs12 sm6>
        <v-card>
          <v-img src="https://www.recetastv.com/wp-content/uploads/2019/03/pizza-hawaiana.jpg" width="600" height="286"></v-img>
          <v-card-title><h2>Pizza Hawaiana</h2></v-card-title>
          <v-card-text>La mejor de nuestra casa pruebala ordena ahora</v-card-text>
          <v-card-actions><v-btn rounded color="info" @click="dialog=!dialog">ordenar</v-btn></v-card-actions>
        </v-card>
      </v-flex>
    </v-layout>

    <v-dialog v-model="dialog" width="200" persistent>
      <v-card>
        <v-card-title>Hey!</v-card-title>
        <v-card-text>Antes de ordenar debes iniciar sesión</v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-btn rounded color="primary" @click="dialog=!dialog">Cerrar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  data: () =>({
    dialog:false
  })
}
</script>
