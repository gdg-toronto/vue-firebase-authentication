<template>
  <v-container class="pt-5" v-if="isLoading">
    <v-layout justify-center>
      <v-progress-circular
        color="accent"
        :indeterminate="true"
      ></v-progress-circular>
    </v-layout>
  </v-container>
  <v-container v-else>
    <v-layout justify-center>Loaded!</v-layout>
    <v-list>
      <template v-for="(item, index) in messages">
        <v-list-tile :key="index">
          <v-list-tile-content>
            <v-list-tile-title v-html="item.displayName"></v-list-tile-title>
            <v-list-tile-sub-title v-html="item.text"></v-list-tile-sub-title>
          </v-list-tile-content>
        </v-list-tile>
      </template>
    </v-list>
  </v-container>
</template>

<script>
  import firebase from "firebase/app"
  import "firebase/firestore"
  
  let db
  export default {
    name: "Hello",
    data: () => ({
      messages: []
    }),
    mounted() {
      db = firebase.firestore()
      db.collection("messages").get().then(
        (result) => {
          result.forEach((entry) => {
            this.messages.push(entry.data())
            console.log(entry.data())
          })
        }
      )
    }
  }
</script>

<style scoped>

</style>
