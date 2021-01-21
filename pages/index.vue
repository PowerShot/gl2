<template>
  <section class="section">
    <div class="columns is-centered">
      <card
        title="Lecture"
      >
        <b-button type="is-success">Facile</b-button>
        <b-button type="is-warning">Moyen</b-button>
        <b-button type="is-danger">Difficile</b-button>
      </card>

      <card
        title="Écriture"
      >
        <b-button type="is-success">Facile</b-button>
        <b-button type="is-warning">Moyen</b-button>
        <b-button type="is-danger">Difficile</b-button>
      </card>

      <card
        title="Calcul"
      >
        <b-button type="is-success">Facile</b-button>
        <b-button type="is-warning">Moyen</b-button>
        <b-button type="is-danger">Difficile</b-button>
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
