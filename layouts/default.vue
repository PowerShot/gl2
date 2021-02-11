<template>
  <div>
    <nav class="navbar is-primary" role="navigation" aria-label="main navigation">
  <div class="navbar-brand">

    <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbarBasicExample">
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
      <span aria-hidden="true"></span>
    </a>
  </div>

  <div class="navbar-menu"
    >
    <div class="navbar-start">
        <a class="navbar-item" href="/">
          <b-icon class="mr-1" icon="home" /> Accueil
        </a>

        <div class="navbar-item has-dropdown is-hoverable"
          v-for="(item, key) of items"
          :key="key">
          <a class="navbar-link" :href="item.to.name">
            <b-icon class="mr-1" :icon="item.icon" /> {{ item.title }}
          </a>
          <div class="navbar-dropdown">
            <a class="navbar-item" :href="item.to.name">
              Facile *
            </a>
            <a class="navbar-item" :href="item.to.name+'?niveau=moyen'">
              Moyen **
            </a>
            <a class="navbar-item"  :href="item.to.name+'?niveau=difficile'">
              Difficile ***
            </a>
          </div>
        </div>
    </div>
    <div class="navbar-end">
          <div class="navbar-item">
            <div class="buttons">
              <a class="button is-primary"  @click="alertJeuSerieu">
                <strong>Qu'es-ce qu'un jeu sérieux ?</strong>
              </a>
              <a class="button is-light" href="/fiche">
                Aide à domicile (fiche métier)
              </a>
            </div>
          </div>
        </div>
  </div>
</nav>
    <!-- <nav class="navbar is-primary">
      <div
        v-for="(item, key) of items"
          :key="key">
        <a class="navbar-item">
          <b-icon class="mr-4" :icon="item.icon" /> {{ item.title }}
        </a>

        <hr class="navbar-divider">
      </div>
    </nav> -->

    <div class="container column hero-body">
        <nuxt />
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      items: [
        {
          title: 'Lecture',
          icon: 'lightbulb',
          to: { name: 'lecture' },
          color: 'is-primary'
        },
        {
          title: 'Écriture',
          icon: 'read',
          to: { name: 'ecriture' },
          color: 'is-primary'
        },
        {
          title: 'Calcul',
          icon: 'calculator-variant',
          to: { name: 'calcul' },
          color: 'is-primary'
        }
      ]
    }
  },
  methods: {
    alertJeuSerieu() {
      this.$buefy.dialog.alert({
          title: "Qu'es-ce qu'un jeu sérieux ?",
          message: "Un <b>jeu sérieux</b> est une activité pédagogique avec des ressorts de divertissement, associant un objectif sérieux.<br> C’est une application informatique, dont l'objectif est de combiner à la fois des aspects sérieux tels, de manière non exhaustive, l'enseignement, l'apprentissage, la communication, ou encore l'information, avec des ressorts ludiques issus du jeu vidéo.<br> Une telle association a donc pour but de s'écarter du simple divertissement.<br><br><a href='http://www.cndp.fr/crdp-reims/index.php?id=2237' target='_blank'>En savoir plus</a>",
          confirmText: 'OK'
      })
    },
  }
}
</script>
