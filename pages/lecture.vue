<template>
  <div>
    <section class="section">
      
      <div class="navbar-end">
          <b-taglist attached>
          <b-tag type="is-success" size="is-large">Facile</b-tag>
          <b-tag type="is-light" size="is-large">5 <b>/ 5</b></b-tag>
      </b-taglist>
      </div>

      <p>{{ this.question["Contenu"]}}</p>
  
      <div class="title m-5">{{ this.question["Question"]}}</div>
      
      <section>
          <b-field>
              <b-checkbox>{{ this.question["Proposition"][0] }}</b-checkbox>
          </b-field>
          <b-field>
              <b-checkbox>{{ this.question["Proposition"][1] }}</b-checkbox>
          </b-field>
          <b-field>
              <b-checkbox>{{ this.question["Proposition"][2] }}</b-checkbox>
          </b-field>
          <b-field>
              <b-checkbox>{{ this.question["Proposition"][3] }}</b-checkbox>
          </b-field>
      </section>
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
        "Contenu" : "La voiture de Jean est rouge, il ne l'allume pas souvent.",
        "Proposition": [
          "Rouge",
          "Bleu",
          "Vert",
          "Jaune"
        ],
        "Correct" :"1",
        "Question": "De quelle couleur est la voiture de Jean ?"
      }
    }
  }
}
</script>
