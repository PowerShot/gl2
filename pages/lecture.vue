<template>
  <div>
    <section class="section">
      <div class="title m-5">Lecture</div>
      <div class="navbar-end">
          <b-taglist attached>
          <b-tag :type="this.couleur_niveau" size="is-large"> {{ this.niveau }}</b-tag>
          <b-tag type="is-light" size="is-large">{{ this.bonne_rep}} <b>/ {{ this.nbr_question}}</b></b-tag>
      </b-taglist>
      </div>

      <p class="m-2">{{ this.question[this.niveau]["texte"] }}</p>

      <section>
        <div class="subtitle m-4">{{ this.question[this.niveau]["questions"][this.pos]['phrase']}}</div>
        <div v-for="i in this.question[this.niveau]['questions'][this.pos]['proposition'].length">
          <b-radio v-model="reponse_text"
                :native-value="i">
                {{ question[niveau]["questions"][pos]["proposition"][i-1]}}
          </b-radio>
        </div>
      </section>
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

      
      let resultat = this.question[this.niveau]["questions"][this.pos]["reponse"]
      if(resultat == this.reponse_text) this.bonne_rep++
      this.nbr_question++
      this.pos++
      

      // changement de niveau
      if(this.pos == this.question[this.niveau]['questions'][this.pos]['proposition'].length) {
        if(this.niveau == "difficile") {
          this.est_fini = true
          this.pos--
        } else {
          this.niveau = (this.niveau == "facile" ? "moyen" : "difficile")
          console.log(this.niveau)
          if(this.niveau == "facile"){
            this.couleur_niveau = "is-success"
          }
          else if(this.niveau == "moyen"){
            this.couleur_niveau = "is-warning"
          }
          else{
            this.couleur_niveau = "is-danger"
          
          }
          this.pos = 0
        }
        
      }
      this.reponse_text = ""

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
  data() {
    return {
      reponse_text: "",
      couleur_niveau: "",
      niveau: "facile",
      bonne_rep: 0,
      nbr_question: 0,
      pos: 0,
      entree: 0.0,
      est_fini: false,
      question: {
        facile: {
          texte: "Le loup est un mammifère de la famille des canidés, et un parent proche du chien domestique.La femelle du loup est la louve, son petit est le louveteau. Le loup hurle.L'habitat historique du loup gris comprend toute l'Amérique du Nord (du Mexique à l'Alaska et au Groenland), toute l'Europe (du nord au sud) et presque toute l'Asie. Il a toujours été absent d'Asie du Sud-Est, d'Océanie, d'Afrique et d'Amérique du Sud.Les loups étaient jadis très répandus dans tout l'hémisphère Nord, mais leur population a été décimée, par la chasse d'une part, mais également suite à l'occupation de leur habitat par l'homme. On peut même parler d'extermination dans la seconde moitié du XIXe siècle en Europe occidentale, après les travaux de Pasteur faisant du loup le principal vecteur sauvage de la rage.Les loups sont des prédateurs, vivant et chassant en meutes organisées, selon une hiérarchie sociale stricte. La meute est dirigée par un mâle et une femelle. Ce couple est généralement le seul à procréer. Ce type d'organisation se retrouve également chez d'autres canidés vivant en meutes, tels que les dholes et les lycaons, respectivement chiens sauvages d'Asie et d'Afrique.Le lien entre le loup et le chien domestique est assez controversé. Certains voient le loup comme l'ancêtre direct du chien, tandis que d'autres considèrent que cet ancêtre serait plutôt le chacal doré. (ref: wikipedia.org)",
          questions: [
            {
              phrase: "Comment s'appelle le petit du loup ?",
              proposition:["Le louveau","Le louveteau","Le louveton"],
              reponse: 2
            },
            {
              phrase: "Le lien entre le loup et le chien domestique est assez controversé, avec quel autre animal le loup pourrait-il être apparenté ?",
              proposition:["Le lion","Le tigre","Le chacal doré"],
              reponse: 3
            },
            {
              phrase: " Qu'est-ce que les dholes ?",
              proposition:["Des loups sauvages","Des chiens sauvages d'asie","Des loups domestiques"],
              reponse: 2
            },
            {
              phrase: "Après les travaux de Pasteur, le loup a été accusé de répandre quelle maladie ?",
              proposition:["La rage","La covid19","La vache folle"],
              reponse: 1
            },
            {
              phrase: " Le loup est un animal solitaire. Vrai ou faux?",
              proposition:["Vrai","Faux","Parfois"],
              reponse: 2
            }
            ]
          },
        moyen: {
          texte:"Les coccinelles figurent parmi les insectes utilisés par l'homme : beaucoup d'espèces se nourrissent en effet de pucerons et sont donc utilisées en lutte biologique comme insecticide naturel. Selon la croyance populaire, le nombre de taches de la coccinelle dépend directement de son âge ; cette information est erronée, le nombre précisant tout simplement l'espèce dont il est une clé d'identification.Dans le langage courant, on appelle aussi la coccinelle « bête à bon Dieu », car elle est la meilleure amie des jardiniers (les anciens prédisaient du beau temps lorsque la coccinelle s’envolait) et surtout, parce que, selon une légende remontant au Moyen Âge, elle porterait bonheur. Ce surnom remonte au Xe siècle. Condamné à mort pour un meurtre commis à Paris, un homme, qui clamait son innocence, a dû son salut à la présence du petit insecte. En effet, le jour de son exécution publique, le condamné devait avoir la tête tranchée. Mais une coccinelle se posa sur son cou. Le bourreau tenta de l’enlever, mais le coléoptère revint à plusieurs reprises se placer au même endroit. Le roi Robert II (972-1031) y vit alors une intervention divine et décida de gracier l’homme. Quelques jours plus tard, le vrai meurtrier fut retrouvé. Cette histoire s’est très vite répandue et la coccinelle fut dès lors considérée comme un porte-bonheur qu’il ne fallait pas écraser.",
          questions: [
            {
              phrase: "Sur quelle partie du condamné à mort se posa la coccinelle ?",
              proposition:["Son cou","Ses jambes","Son dos"],
              reponse: 1
            },
            {
              phrase: "Le nombre de taches sur la coccinelle définit son âge, vrai ou faux ?",
              proposition:["Vrai","Faux","Parfois"],
              reponse: 2
            },
            {
              phrase: "De quoi se nourrit la coccinelle dans les jardins, qui ravit les jardiniers ?",
              proposition:["Les Abeilles","Les Frelons","Les Pucerons"],
              reponse: 3
            },
            {
              phrase: "À quand remonte la légende de la bête à bon Dieu ?",
              proposition:["Il y a quelques années ","Moyen âge","Il y a 100 ans"],
              reponse: 1
            },
            {
              phrase: "Selon les anciens, lorsque la coccinelle s'envolait, comment allait être le temps ?",
              proposition:["Beau","Orageux ","Les deux"],
              reponse: 1
            }
          ]
        },
        difficile: {
          texte:"L'ours blanc, aussi connu sous le nom d'ours polaire, est un grand mammifère omnivore (à prédominance carnivore) originaire des régions arctiques. C'est, avec l'ours kodiak et l'éléphant de mer, l'un des plus grands carnivores terrestres et il figure au sommet de sa pyramide alimentaire.Parfaitement adapté à son habitat, l'ours blanc possède une épaisse couche de graisse ainsi qu'une fourrure qui l'isolent du froid. La couleur blanche de son pelage lui assure un camouflage idéal sur la banquise et sa peau noire lui permet de mieux conserver sa chaleur corporelle. Pourvu d'une courte queue et de petites oreilles, il possède une tête relativement petite et fuselée ainsi qu'un corps allongé, caractéristiques de son adaptation à la natation. L'ours blanc est un mammifère marin semi-aquatique, dont la survie dépend essentiellement de la banquise et de la productivité marine. Il chasse aussi bien sur terre que dans l'eau. Son espérance de vie est de 15 à 30 ans.Cette espèce vit uniquement sur la banquise autour du pôle Nord, au bord de l'océan Arctique. En raison du réchauffement climatique et du bouleversement de cet habitat, les populations d'ours blancs sont globalement en déclin et l'espèce est considérée comme en danger. On estime la population d'ours blancs entre 20 000 et 25 000 individus.Animal charismatique, l'ours blanc a un fort impact culturel sur les peuples inuits, qui dépendent toujours de sa chasse pour survivre. Il a également marqué la culture populaire via certains de ses représentants comme Knut, ou encore l'art avec la sculpture d'ours blanc réalisée par François Pompon. ",
          questions: [
            {
              phrase: "L'océan Arctique est situé à quel pôle ?",
              proposition:["nord","sud","est"],
              reponse: 1

            },
            {
              phrase: "Avec quelle autre race d'ours, l'ours blanc est-il l'un des plus grands carnivores terrestres ? l'ours :",
              proposition:["kellogs ","kodiak","ours brun"],
              reponse: 2
            },
            {
              phrase: "Où l'ours blanc chasse-t-il ?",
              proposition:["sur la banquise et dans l'eau","en fôret","les deux"],
              reponse: 1
            },
            {
              phrase: "Quelle peuplade vit dans la même région que l'ours polaire ?",
              proposition:["massaïs","aucun","inuits"],
              reponse: 3
            },
            {
              phrase: "l'ours blanc a-t-il une couche de graisse ?",
              proposition:["non","oui","parfois"],
              reponse: 2
            }
          ]
        }
      }
    }
  }
}
</script>