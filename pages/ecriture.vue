<template>
  <div>
    
    <section class="section">
      <div class="title m-5">{{ this.nom_jeu}}</div>
      <div class="navbar-end">
          <b-taglist attached>
          <b-tag :type="this.couleur_niveau" size="is-large"> {{ this.niveau }} </b-tag>
          <b-tag type="is-light" size="is-large">{{ this.bonne_rep }} <b>/ {{ this.nbr_question }}</b></b-tag>
      </b-taglist>
      </div>
    </section>
    <section class="section">
    <!-- Facile -->
      <div v-if="this.niveau=='facile'">
        <section class="section rows is-centered">
          <div class="is-centered columns">
            <img width="200px" :src="this.question[this.niveau][this.pos]['image']">
          </div>
          <b-field label="Réponse :">
              <b-input width="200px" v-model="reponse_text"></b-input>
          </b-field>
        </section>
      </div>
    <!-- Moyen -->
      <div v-else-if="this.niveau=='moyen'">
        <section class="section is-centered rows">
          <div class="columns">
            <div class="subtitle mr-3">{{ question["moyen"][this.pos]["question-p1"] }}</div>
            <b-input v-model="reponse_text"></b-input>
            <div class="subtitle ml-3">{{ question["moyen"][this.pos]["question-p2"] }}</div>
          </div>
        </section>
      </div>
    
    <!-- Difficile -->
      <div v-else>
        <div class="title m-5">{{ this.question['difficile'][this.pos]['question']}}</div>
        <div v-for="i in this.question['difficile'][this.pos]['proposition'].length">
          <b-radio v-model="reponse_text"
                :native-value="i">
                {{ question["difficile"][pos]["proposition"][i-1] }}
          </b-radio>
        </div>
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
  methods: {
    verifier: function() {

      
      let resultat = this.question[this.niveau][this.pos]["reponse"]
      if(resultat == this.reponse_text) this.bonne_rep++
      
      this.nbr_question++
      this.pos++
      

      // changement de niveau
      if(this.pos == this.question[this.niveau].length) {
        if(this.niveau == "difficile") {
          this.est_fini = true
          this.pos--
        } else {
          this.niveau = (this.niveau == "facile" ? "moyen" : "difficile")
          console.log(this.niveau)
          if(this.niveau == "facile"){
            this.couleur_niveau = "is-success"
            this.nom_jeu = "Question de vocabulaire"
          }
          else if(this.niveau == "moyen"){
            this.couleur_niveau = "is-warning"
            this.nom_jeu = "Question de conjugaison"
          }
          else{
            this.couleur_niveau = "is-danger"
            this.nom_jeu = "Question d'orthograhe"
          
          }
          this.pos = 0
        }
      }
      this.reponse_text = ""

    }
  },
  mounted: function() {
    if(this.niveau == "facile") this.couleur_niveau = "is-success"
    else if(this.niveau == "moyen") this.couleur_niveau = "is-warning"
    else this.couleur_niveau = "is-danger"
  },
  created: function() {
    this.niveau = this.$route.query.niveau
    if(this.niveau == undefined) this.niveau = "facile"
  },
  data() {
    return {
      nom_jeu: "Question de vocabulaire",
      reponse_text: "",
      couleur_niveau: "",
      niveau: "facile",
      bonne_rep: 0,
      nbr_question: 0,
      pos: 0,
      entree: 0.0,
      est_fini: false,
      question: {
        "facile":[
            {
                "image" : "https://cdn.jysk.fr/media/catalog/product/cache/8/thumbnail/960x/d34aaef3401395db2614ec4ce2acbbee/5/0/50814004_3_.jpg",
                "reponse": "pomme"
            },
            {
                "image" : "https://www.lesfruitsetlegumesfrais.com/_upload/cache/ressources/produits/carotte/carotte_346_346_filled.jpg",
                "Reponse": "carotte"
            },
            {
                "image" : "https://cdn.futura-sciences.com/buildsv6/images/wide1920/1/d/8/1d8a8e8fe1_109430_chouette-hibou-difference.jpg",
                "reponse": "chouette"
            },
            {
                "image" : "https://media2.labovida.com/10034-large_default/cuillere-a-cafe-rossini.jpg?cache=2",
                "reponse": "cuillère"
            },
            {
                "image" : "https://www.atelierdeschefs.com/media/ingredient-e279-le-chocolat.jpg",
                "reponse": "chocolat"
            }
        ],
        "moyen":[
            {
                "question-p1": "Il a ",
                "question-p2": "y aller. (falloir)",
                "reponse": "fallu"
            },
            {
                "question-p1": "Nous n'avons pas ",
                "question-p2": "réussir. (pouvoir)",
                "reponse": "pu"
            },
            {
                "question-p1": "Tu as ",
                "question-p2": "une bonne idée. (avoir)",
                "reponse": "eu"
            },
            {
                "question-p1": "On a ",
                "question-p2": "les urgences. (appeler)",
                "reponse": "appelé"
            },
            {
                "question-p1": "Vous avez ",
                "question-p2": "tout le magasin. (acheter)",
                "reponse": "acheté"
            }
        ],
        "difficile":[
            {
                "question" : "Mon frère et moi, depuis deux jours...",
                "proposition":[
                    "sommes obligés de descendre par l'escalier.",
                    "bloque le pont.",
                    "est revenue vers 20 heures"
                ],
                "reponse" : "1"
            },
            {
                "question" : "Les clientes du magasin...",
                "proposition":[
                    "sommes obligés de descendre par l'escalier.",
                    "attendent près de la porte d'entrée.",
                    "se sont perdues en mer."
                ],
                "reponse" : "2"
            },
            {
                "question" : "Pour l'exposition, les photos...",
                "proposition":[
                    "décollent un par un de l'aéroport.",
                    "sont retirés de la course.",
                    "sont accrochées au mur."
                ],
                "reponse" : "3"
            },
            {
                "question" : "Avec la tempête, les goélettes...",
                "proposition":[
                    "attendent près de la porte d'entrée.",
                    "sont retirés de la course.",
                    "se sont perdues en mer."
                ],
                "reponse" : "3"
            },
            {
                "question" : "Depuis l'avalanche, la neige...",
                "proposition":[
                    "bloque le pont.",
                    "est revenue vers 20 heures.",
                    "sommes obligés de descendre par l'escalier."
                ],
                "reponse" : "1"
            }
        ]
      }
    }
  }
}
</script>
