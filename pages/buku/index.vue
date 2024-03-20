<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-lg-12">
        <h2 class="text-center my-4">BUKU</h2>
        <div class="my-3">
          <form @submit.prevent="getBooks">
          <input v-model="keyword" type="search" class="form-control rounded-3" placeholder="Mau Baca Apa Hari Ini?">
          </form>
        </div>
        <div class="my-3 text-muted">menampilkan 3 dari 3</div>
        <div class="row">
        <!-- <div v-for="(book,i) in books" :key="i" class="col-lg-2">
          <div class="card mb-3">
            <div class="card-body">
              <nuxt-link to="/rincian/buku1">
              <img src="~/assets/img/cover1.jpg" class="cover" alt="cover 1">
              </nuxt-link>
            </div>
          </div>
          </div>
          <div v-for="(book,i) in books" :key="i" class="col-lg-2">
          <div class="card mb-3">
            <div class="card-body">
              <img src="~/assets/img/cover2.jpeg" class="cover" alt="cover 2">
            </div>
          </div>
          </div> -->
          <div v-for="(book,i) in books" :key="i" class="col-lg-2">
          <div class="card mb-3">
            <div class="card-body">
              <h3>{{ book.judul }}</h3>
            </div>
          </div>
          </div>
        </div>
      </div>
      <nuxt-link to="/">
          <button type="submit" class="btn btn-dark rounded-3 px-5">Kembali</button>
        </nuxt-link>
    </div>
  </div>
</template>

<style scoped>

.cover{
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: 0 30;
}
</style>

<script setup>

const supabase = useSupabaseClient()

const books = ref([])
const keyword = ref([])

const getBooks = async () => {
  const { data, error } = await supabase.from('buku').select(`*, kategori(*)`)
  .ilike('judul', `%${keyword.value}%`)
  if(data) books.value = data
}

onMounted(() => {
  getBooks()
})
</script>