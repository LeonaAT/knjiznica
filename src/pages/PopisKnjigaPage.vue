
<template>
  <q-page class="library-page q-pa-lg">
    <div class="page-heading q-mb-xl">
      <div class="text-overline text-green-8">GRADSKA KNJIŽNICA</div>
      <div class="text-h3 text-weight-bold heading-title">
        Naša kolekcija knjiga
      </div>
      <p class="text-subtitle1 text-grey-7">
        Otkrijte nove svjetove, zanimljive priče i svoje sljedeće omiljeno štivo.
      </p>
    </div>

    <div class="row q-col-gutter-md q-mb-xl">
      <div class="col-12 col-md-4">
        <q-card class="info-card">
          <q-card-section class="row items-center">
            <q-icon name="menu_book" size="38px" color="green-8" />
            <div class="q-ml-md">
              <div class="text-h5 text-weight-bold">6</div>
              <div class="text-grey-7">Knjiga u kolekciji</div>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div class="col-12 col-md-4">
        <q-card class="info-card">
          <q-card-section class="row items-center">
            <q-icon name="auto_stories" size="38px" color="orange-8" />
            <div class="q-ml-md">
              <div class="text-h5 text-weight-bold">5</div>
              <div class="text-grey-7">Različitih žanrova</div>
            </div>
          </q-card-section>
        </q-card>
      </div>

      <div class="col-12 col-md-4">
        <q-card class="info-card">
          <q-card-section class="row items-center">
            <q-icon name="favorite" size="38px" color="pink-6" />
            <div class="q-ml-md">
              <div class="text-h5 text-weight-bold">Za svakoga</div>
              <div class="text-grey-7">Nešto zanimljivo</div>
            </div>
          </q-card-section>
        </q-card>
      </div>
    </div>

    <div class="text-h5 text-weight-bold q-mb-md">
      <q-icon name="library_books" color="green-8" />
      Popis svih knjiga
    </div>

    <q-table
      :rows="books"
      :columns="columns"
      row-key="id"
      flat
      class="book-table"
      :pagination="{ rowsPerPage: 6 }"
    >
      <template v-slot:body-cell-title="props">
        <q-td :props="props">
          <span class="text-weight-bold">{{ props.value }}</span>
        </q-td>
      </template>

      <template v-slot:body-cell-status="props">
        <q-td :props="props">
          <q-badge
            color="green-1"
            text-color="green-9"
            rounded
            class="q-pa-sm"
          >
            {{ props.value }}
          </q-badge>
        </q-td>
      </template>
    </q-table>
  </q-page>
</template>

<script setup>
const columns = [
  { name: 'id', label: 'ID', field: 'id', align: 'left' },
  { name: 'title', label: 'Naziv knjige', field: 'title', align: 'left' },
  { name: 'author', label: 'Autor', field: 'author', align: 'left' },
  { name: 'genre', label: 'Žanr', field: 'genre', align: 'left' },
  { name: 'year', label: 'Godina', field: 'year', align: 'left' },
  { name: 'status', label: 'Dostupnost', field: 'status', align: 'left' }
]

const books = [
  { id: 1, title: 'Mali princ', author: 'Antoine de Saint-Exupéry', genre: 'Fantastika', year: 1943, status: 'Dostupna' },
  { id: 2, title: 'Harry Potter', author: 'J. K. Rowling', genre: 'Fantastika', year: 1997, status: 'Dostupna' },
  { id: 3, title: 'Zločin i kazna', author: 'Fjodor Dostojevski', genre: 'Roman', year: 1866, status: 'Posuđena' },
  { id: 4, title: '1984.', author: 'George Orwell', genre: 'Distopija', year: 1949, status: 'Dostupna' },
  { id: 5, title: 'Alkemičar', author: 'Paulo Coelho', genre: 'Roman', year: 1988, status: 'Dostupna' },
  { id: 6, title: 'Mali život', author: 'Hanya Yanagihara', genre: 'Drama', year: 2015, status: 'Posuđena' }
]
</script>

<style scoped>
.library-page {
  background: #f7f5ef;
  min-height: 100%;
}

.heading-title {
  color: #254b3b;
  margin-top: 8px;
}

.info-card {
  border-radius: 16px;
  background: white;
  box-shadow: 0 4px 18px rgba(0, 0, 0, 0.04);
}

.book-table {
  border-radius: 16px;
  overflow: hidden;
  background: white;
}

:deep(.q-table thead tr) {
  background: #e8eee8;
  color: #254b3b;
  font-weight: bold;
}

:deep(.q-table tbody td) {
  padding: 16px 12px;
}
</style>
