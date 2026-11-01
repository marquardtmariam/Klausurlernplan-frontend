<script setup>
import { ref } from 'vue'

const klausuren = ref([
  {
    id: 1,
    fach: 'Webtechnologien',
    datum: '2027-02-10',
    themen: [
      { id: 1, titel: 'HTML & CSS Grundlagen', erledigt: true },
      { id: 2, titel: 'JavaScript & DOM', erledigt: false },
      { id: 3, titel: 'Vue.js Komponenten', erledigt: false },
    ],
  },
  {
    id: 2,
    fach: 'Programmieren 2',
    datum: '2027-02-17',
    themen: [
      { id: 4, titel: 'Vererbung & Interfaces', erledigt: false },
      { id: 5, titel: 'Design Patterns', erledigt: false },
    ],
  },
  {
    id: 3,
    fach: 'Modellierung von Anwendungssystemen',
    datum: '2027-02-24',
    themen: [
      { id: 6, titel: 'BPMN', erledigt: true },
      { id: 7, titel: 'Business Model Canvas', erledigt: true },
    ],
  },
])

function anzahlErledigt(klausur) {
  return klausur.themen.filter((thema) => thema.erledigt).length
}
</script>

<template>
  <section>
    <h2>Meine Klausuren</h2>

    <ul class="klausuren">
      <li v-for="klausur in klausuren" :key="klausur.id" class="klausur">
        <h3>
          {{ klausur.fach }}
          <small>({{ klausur.datum }})</small>
        </h3>
        <p>{{ anzahlErledigt(klausur) }} von {{ klausur.themen.length }} Themen erledigt</p>

        <ul class="themen">
          <li v-for="thema in klausur.themen" :key="thema.id">
            <label :class="{ erledigt: thema.erledigt }">
              <input type="checkbox" v-model="thema.erledigt" />
              {{ thema.titel }}
            </label>
          </li>
        </ul>
      </li>
    </ul>
  </section>
</template>

<style scoped>
.klausuren,
.themen {
  list-style: none;
  padding: 0;
}
.klausur {
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 1rem;
  margin-bottom: 1rem;
}
.erledigt {
  text-decoration: line-through;
  opacity: 0.6;
}
</style>
