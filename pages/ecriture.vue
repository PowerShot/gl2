<template>
  <div>
    <section class="section">
      
      <div class="navbar-end">
          <b-taglist attached>
          <b-tag type="is-success" size="is-large">Facile</b-tag>
          <b-tag type="is-light" size="is-large">5 <b>/ 5</b></b-tag>
      </b-taglist>
      </div>
    
    </section>
    <section class="section is-centered">
      <img width="200px" :src="this.question['Image']">
      <b-field label="Mot">
          <b-input width="200px" v-model="name"></b-input>
      </b-field>
    </section>

    <div>
        <b-button size="is-medium" class="is-success"
                  icon-left="check">
                  Valider
              </b-button>
        <b-button size="is-medium" class="is-light"
                  icon-left="home">
                  Accueil
              </b-button>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      question: {
        "id" : 1,
        "Image" : "https://cdn.jysk.fr/media/catalog/product/cache/8/thumbnail/960x/d34aaef3401395db2614ec4ce2acbbee/5/0/50814004_3_.jpg",
        "Reponse": "pomme"
      }
    }
  }
}
</script>
