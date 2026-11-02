
<template>
  <q-page class="search-page q-pa-lg">
    <div class="q-mb-xl">
      <div class="text-overline text-green-8">GRADSKA KNJIŽNICA</div>
      <div class="text-h3 text-weight-bold heading-title">
        Pronađi svoju knjigu
      </div>
      <p class="text-subtitle1 text-grey-7">
        Upiši naziv knjige ili ime autora i pronađi svoju sljedeću priču.
      </p>
    </div>

    <q-card class="search-card q-pa-md q-mb-xl">
      <q-card-section>
        <div class="text-h6 text-weight-bold q-mb-md">
          <q-icon name="search" color="green-8" size="28px" />
          Pretraživanje knjiga
        </div>

        <q-input
          v-model="searchText"
          outlined
          rounded
          placeholder="Upiši naziv knjige ili autora..."
          bg-color="white"
        >
          <template v-slot:prepend>
            <q-icon name="search" color="green-8" />
          </template>
        </q-input>

        <div class="q-mt-md text-weight-medium">
          Pretražuj prema:
        </div>

        <q-option-group
          v-model="searchType"
          :options="[
            { label: 'Nazivu knjige', value: 'title' },
            { label: 'Autoru', value: 'author' }
          ]"
          color="green-8"
          inline
        />

        <q-btn
          label="Traži knjigu"
          icon="search"
          color="green-9"
          rounded
          unelevated
          class="q-mt-md full-width"
          @click="searchBooks"
        />
      </q-card-section>
    </q-card>

    <div class="text-h5 text-weight-bold q-mb-md">
      Rezultati pretraživanja
    </div>

    <q-card class="result-card">
      <q-card-section v-if="results.length === 0" class="text-center q-pa-xl">
        <q-icon name="menu_book" size="55px" color="grey-5" />
        <div class="text-h6 q-mt-md">Nema pronađenih knjiga</div>
        <div class="text-grey-7">Pokušaj s drugim pojmom.</div>
      </q-card-section>

      <q-list v-else separator>
        <q-item v-for="book in results" :key="book.id" class="q-pa-md">
          <q-item-section avatar>
            <q-icon name="auto_stories" size="32px" color="green-8" />
          </q-item-section>

          <q-item-section>
            <q-item-label class="text-weight-bold">
              {{ book.title }}
            </q-item-label>
            <q-item-label caption>
              {{ book.author }} · {{ book.genre }}
            </q-item-label>
          </q-item-section>

          <q-item-section side>
            <q-badge
              :color="book.status === 'Dostupna' ? 'green-1' : 'orange-1'"
              :text-color="book.status === 'Dostupna' ? 'green-9' : 'orange-9'"
            >
              {{ book.status }}
            </q-badge>
          </q-item-section>
        </q-item>
      </q-list>
    </q-card>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const searchText = ref('')
const searchType = ref('title')

const books = [
  { id: 1, title: 'Mali princ', author: 'Antoine de Saint-Exupéry', genre: 'Fantastika', status: 'Dostupna' },
  { id: 2, title: 'Harry Potter', author: 'J. K. Rowling', genre: 'Fantastika', status: 'Dostupna' },
  { id: 3, title: 'Zločin i kazna', author: 'Fjodor Dostojevski', genre: 'Roman', status: 'Posuđena' },
  { id: 4, title: '1984.', author: 'George Orwell', genre: 'Distopija', status: 'Dostupna' },
  { id: 5, title: 'Alkemičar', author: 'Paulo Coelho', genre: 'Roman', status: 'Dostupna' },
  { id: 6, title: 'Mali život', author: 'Hanya Yanagihara', genre: 'Drama', status: 'Posuđena' }
]

const results = ref([])

function searchBooks() {
  const term = searchText.value.trim().toLowerCase()

  if (!term) {
    results.value = []
    return
  }

  results.value = books.filter(book =>
    book[searchType.value].toLowerCase().includes(term)
  )
}
</script>

<style scoped>
.search-page {
  background: #f7f5ef;
  min-height: 100%;
}

.heading-title {
  color: #254b3b;
  margin-top: 8px;
}

.search-card,
.result-card {
  border-radius: 18px;
  background: white;
  box-shadow: 0 4px 18px rgba(0, 0, 0, 0.04);
}
</style>

