<template>
  <div class="bell-test">
    <header class="bell-test-header">
      <h1>Recette de salade de fruits</h1>
    </header>
    <section class="bell-test-recipe">
      <div class="bell-test-recipe--selector">
        <label for="recipeSelector">Choisis le nombre de portion:</label>
        <select id="recipeSelector" tabindex="0" v-model="nbPortionSelected">
          <option v-for="nbPortion in nbPortionMax" v-bind:selected="[ nbPortion === nbPortionSelected ? 'selected' : '' ]" v-bind:key="nbPortion">{{ nbPortion }}</option> // default 2
        </select>
      </div>
      <ul class="bell-test-recipe--list">
        <li>{{nbPortionSelectedQuarter.display}} {{ $tc('cup', nbPortionSelectedQuarter.value)}} ( {{60 * nbPortionSelected }}ml) d'ananas</li>
        <li>{{nbPortionSelectedHalf.display}} {{ $tc('pear', nbPortionSelectedHalf.value)}} </li>
        <li>{{nbPortionSelectedHalf.display}} {{ $tc('spoon', nbPortionSelectedHalf.value)}} ({{15 * nbPortionSelected}} ml) de jus de pommes</li>
        <li>{{ $tc('grape', nbPortionSelected) }} de raisins rouges</li>
        <li>{{70 * nbPortionSelected}} g de fraises</li>
      </ul>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Recipe',
  props: {
    nbPortionMax: {
      type: Number,
      default: 4
    }
  },
  data: function () {
    return {
      nbPortionSelected: 2
    }
  },
  methods: {
    pgcd: function (a, b) {
      if (b) {
        return this.pgcd(b, a % b)
      } else {
        return Math.abs(a)
      }
    }
  },
  computed: {
    nbPortionSelectedHalf: function () {
      const pgcd = this.pgcd(this.nbPortionSelected, 2)
      return {
        display: this.nbPortionSelected % 2 ? `${this.nbPortionSelected / pgcd}/${2 / pgcd}` : this.nbPortionSelected / 2,
        value: Math.floor(this.nbPortionSelected / 2)
      }
    },
    nbPortionSelectedQuarter: function () {
      const pgcd = this.pgcd(this.nbPortionSelected, 4)
      return {
        display: this.nbPortionSelected % 4 ? `${this.nbPortionSelected / pgcd}/${4 / pgcd}` : this.nbPortionSelected / 4,
        value: Math.floor(this.nbPortionSelected / 4)
      }
    }
  }
}
</script>

<style scoped lang="scss">
  .bell-test {
    max-width: 640px;
    margin: 60px auto;
  }
</style>
