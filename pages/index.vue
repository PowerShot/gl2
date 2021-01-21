<template>
  <section class="section">
    <div class="columns is-centered">
      <card
        title="Lecture"
      >
        <a href="lecture?niveau=facile"><b-button type="is-success">Facile</b-button></a>
        <a href="lecture?niveau=moyen"><b-button type="is-warning">Moyen</b-button></a>
        <a href="lecture?niveau=difficile"><b-button type="is-danger">Difficile</b-button></a>
      </card>

      <card
        title="Écriture"
      >
        <div class="rows">
          <a href="ecriture?niveau=facile"><b-button type="is-success">Facile (Vocabulaire)</b-button></a>
          <a href="ecriture?niveau=moyen"><b-button type="is-warning">Moyen (Conjugaison)</b-button></a>
          <a href="ecriture?niveau=difficile"><b-button type="is-danger">Difficile (Orthographe)</b-button></a>
        </div>
      </card>

      <card
        title="Calcul"
      >
        <a href="calcul?niveau=facile"><b-button type="is-success">Facile</b-button></a>
        <a href="calcul?niveau=moyen"><b-button type="is-warning">Moyen</b-button></a>
        <a href="calcul?niveau=difficile"><b-button type="is-danger">Difficile</b-button></a>
      </card>

    </div>
  </section>
</template>

<script>
import Card from '~/components/Card'

export default {
  name: 'HomePage',
  components: {
    Card
  }
}
</script>
