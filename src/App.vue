<template id="app">
  <v-app>
    <v-container>
      <AppForm/>

    </v-container>
  </v-app>
</template>


<style>
@font-face {
  font-family: 'b nazanin';
  src: url('http://cdn.bayan.ir/blog/templates/shared/fonts/BNazanin.eot?view#iefix') format('embedded-opentype'),
  url('http://cdn.bayan.ir/blog/templates/shared/fonts/BNazanin.woff?view') format('woff'),
  url('http://cdn.bayan.ir/blog/templates/shared/fonts/BNazanin.ttf?view') format('truetype');
}

#app {
  font-family: 'b nazanin';
}


</style>
<script>
import AppForm from "@/components/AppForm";
export default {
  components: { AppForm}
}
</script>
