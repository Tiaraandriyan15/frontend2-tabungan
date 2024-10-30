<template>
<div class="container">
  <div class="row justify-content-center my-5">
      <div class="col">
        <div class="card text-bg-primary mb-3" style="max-width: 18rem;">
            <div class="card-header">Jumlah Siswa</div>
            <div class="card-body">
              <p class="card-text fs-1">{{ jumlahSiswa.count }} Siswa</p>
            </div>
        </div>
      </div>
      <div class="col">
        <div class="card text-bg-danger mb-3" style="max-width: 18rem;">
            <div class="card-header">Jumlah Pemasukan</div>
            <div class="card-body">
              <p class="card-text fs-1">{{ jumlah }}Pemasukan</p>
            </div>
        </div>
      </div>
      <div class="col">
        <div class="card text-bg-warning mb-3" style="max-width: 18rem;">
            <div class="card-header">Jumlah Penarikan</div>
            <div class="card-body">
              <p class="card-text fs-1">{{ jum }}Penarikan</p>
            </div>
        </div>
      </div>
</div>
</div>
<!-- </div>  -->
</template>

<script setup>
const supabase = useSupabaseClient()

const jumlahSiswa = ref(0)
const jumlahPemasukan = ref(0)
const jumlahPenarikan = ref(0)
const jum = ref(0)
const jumlah = ref(0)


async function ambilJumlahSiswa() {
  const { data, error } = await supabase
    .from('dashboard_jumlah_siswa')
    .select()
    .single()
  if(data) jumlahSiswa.value = data
}

const getjumlah = async () => {
    const { data, count } = await supabase.from('keluar').select("*", {count: "exact"})
    if (data) jum.value = count
}

const gettotal = async () => {
    const { data, count } = await supabase.from('nabung').select("*", {count: "exact"})
    if (data) jumlah.value = count
}


// async function ambilJumlahPemasukan() {
//   const { data, error } = await supabase
//     .from('nabung')
//     .select()
//     .single()
//   if(data) jumlahPemasukan.value = data
// }

// async function ambilJumlahPenarikan() {
//   const { data, error } = await supabase
//     .from('keluar')
//     .select("*", {count: "exact"})
//     .single()
//   if(data) jumlahPenarikan.value = data
// }

onMounted(() => {
  ambilJumlahSiswa()
  // ambilJumlahPemasukan()
  // ambilJumlahPenarikan()
  getjumlah()
  gettotal()
})
</script>