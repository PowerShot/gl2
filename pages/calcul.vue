<template>
  <div class="is-max-desktop">
    <section class="section">
      <div class="title m-5">Calcul</div>
      <div class="navbar-end">
        <b-taglist attached>
          <!-- Niveau -->
          <b-tooltip label="Niveau"
            position="is-bottom">
            <a><b-tag :type="this.couleur_niveau" size="is-large"> {{ this.niveau }} </b-tag></a>
          </b-tooltip>

          <!-- Score -->
          <b-tooltip label="Score"
            position="is-bottom">
            <a><b-tag type="is-light" size="is-large">{{ this.bonne_rep }} <b>/ {{ this.nbr_question}}</b></b-tag></a>
          </b-tooltip>

          <!-- Didacticiel -->
          <b-tooltip position="is-left" multilined>
            <a><b-tag type="is-info" size="is-large">?</b-tag></a>
            <template v-slot:content>
              <!-- Facile -->
              <!-- Moyen -->
              <!-- Difficile -->
                <b>Résoudre le calcul</b> et <b>insérer</b> le résultat, puis valider.
            </template>
          </b-tooltip>
        </b-taglist>
      </div>

      <div class="container columns is-centered">
        <h1 class="title is-1 mr-3">{{ this.question[this.niveau][this.pos]["calcul"]}} =</h1>
        <b-field class="mt-3">
            <b-input placeholder="Résultat"
                v-model="entree"
                type="number"
                step="0.001">
            </b-input>
        </b-field>
      
      </div>
    </section>
    <div v-if="this.est_fini">
      <a href="/">
      <b-button size="is-large" class="is-light"
                  icon-left="home">
                  Accueil
              </b-button>
      </a>
      </div>
    <div v-else>
      <b-button  size="is-large" class="is-success"
                  icon-left="check"
                  @click="verifier">
                  Valider
              </b-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      couleur_niveau: "is-success",
      niveau: "facile",
      bonne_rep: 0,
      nbr_question: 0,
      pos: 0,
      entree: 0.0,
      est_fini: false,
      question: {
        facile:[
          {
            calcul: "83 - 14",
            reponse: 69
          },
          {
            calcul: "8 + 96",
            reponse: 104
          },
          {
            calcul: "7 * 8",
            reponse: 56
          },
          {
            calcul: "11 * 11",
            reponse: 121
          },
          {
            calcul: "49 / 7",
            reponse: 7
          },
        ],
        moyen: [
          {
            calcul: "12.75 + 3.25",
            reponse: 16
          },
          {
            calcul: "725 + 375",
            reponse: 1100
          },
          {
            calcul: "1.25 * 4",
            reponse: 5
          },
          {
            calcul: "1 / 4",
            reponse: 0.25
          },
          {
            calcul: "7.77 + 3.33 + 9.90",
            reponse: 21
          }
        ],
        difficile: [
          {
            calcul: "7 * 3 * 3 / 9",
            reponse: 7
          },
          {
            calcul: "99 / 2 + 101 / 2",
            reponse: 100
          },
          {
            calcul: "375 / 3",
            reponse: 125
          },
          {
            calcul: "125 * 200",
            reponse: 25000
          },
          {
            calcul: "1 + 2 * 3 - 4 / 5",
            reponse: 6.2
          }
        ]
      }
    }
  },
  created: function() {
    this.niveau = this.$route.query.niveau
    if(this.niveau == undefined) this.niveau = "facile"
  },
  mounted: function() {
    if(this.niveau == "facile") this.couleur_niveau = "is-success"
    else if(this.niveau == "moyen") this.couleur_niveau = "is-warning"
    else this.couleur_niveau = "is-danger"
  },
  methods: {
    verifier: function() {
      let resultat = this.question[this.niveau][this.pos]["reponse"]
      if(resultat == this.entree){
        this.nbr_question++
        this.bonne_rep++
        this.pos++
      }else{
        this.nbr_question++
        this.pos++
      }
      this.entree=0

      if(this.pos == this.question[this.niveau].length) {
        if(this.niveau == "difficile") {
          this.est_fini = true
          this.pos--
        } else {
          this.niveau = (this.niveau == "facile" ? "moyen" : "difficile")
          console.log(this.niveau)
          if(this.niveau == "facile") this.couleur_niveau = "is-success"
          else if(this.niveau == "moyen") this.couleur_niveau = "is-warning"
          else this.couleur_niveau = "is-danger"
          this.pos = 0
        }
      }
    }
  }
}
</script>
