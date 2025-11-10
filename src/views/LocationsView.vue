<template>
  <div class="locations-page">
    <h1 class="title">Locaciones del universo de Rick & Morty</h1>

    <!-- Buscador y Filtro -->
    <div class="filter-bar">
      <input
        v-model="searchTerm"
        type="text"
        placeholder="Buscar por nombre..."
        class="search-input"
      />
      <select v-model="typeFilter" class="filter-select">
        <option value="all">Todos los tipos</option>
        <option value="Planet">Planeta</option>
        <option value="Space station">Estaciones espaciales</option>
        <option value="Cluster">Cúmulos</option>
        <option value="Microverse">Microversos</option>
      </select>
    </div>

    <!-- Grid de locaciones -->
    <div class="locations-grid">
      <div
        v-for="loc in filteredLocations"
        :key="loc.id"
        class="location-card"
      >
        <h3 class="location-name">{{ loc.name }}</h3>
        <div class="location-info">
          <p><strong>Tipo:</strong> {{ loc.type }}</p>
          <p><strong>Dimensión:</strong> {{ loc.dimension }}</p>
          <p><strong>Residentes:</strong> {{ loc.residents.length }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LocationsView',

  data() {
    return {
      locations: [],
      searchTerm: '',
      typeFilter: 'all'
    }
  },

  computed: {
    filteredLocations() {
      return this.locations.filter(loc => {
        const matchesType =
          this.typeFilter === 'all' || loc.type === this.typeFilter
        const matchesName = loc.name
          .toLowerCase()
          .includes(this.searchTerm.toLowerCase())
        return matchesType && matchesName
      })
    }
  },

  async mounted() {
    try {
      const response = await fetch('https://rickandmortyapi.com/api/location')
      const data = await response.json()
      this.locations = data.results
      console.log('✅ Locaciones cargadas:', this.locations)
    } catch (error) {
      console.error('❌ Error al cargar locaciones:', error)
    }
  }
}
</script>

<style scoped>
.locations-page {
  padding: 40px;
  text-align: center;
  background-color: #f4f7fb;
  min-height: 100vh;
}

/* === Título === */
.title {
  font-size: 2rem;
  font-weight: bold;
  color: #1a1a1a;
  margin-bottom: 30px;
}

/* === Filtros === */
.filter-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  margin-bottom: 40px;
  flex-wrap: wrap;
}

.search-input {
  padding: 12px 16px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 8px;
  width: 280px;
  outline: none;
  transition: 0.3s;
}

.search-input:focus {
  border-color: #00c7ff;
  box-shadow: 0 0 6px rgba(0, 199, 255, 0.4);
}

.filter-select {
  padding: 12px 14px;
  font-size: 16px;
  border-radius: 8px;
  border: 1px solid #ccc;
  outline: none;
  background-color: white;
  transition: 0.3s;
}

.filter-select:focus {
  border-color: #00c7ff;
  box-shadow: 0 0 6px rgba(0, 199, 255, 0.4);
}

/* === Cuadrícula === */
.locations-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 25px;
  justify-items: center;
}

/* === Tarjetas de locaciones === */
.location-card {
  background: #ffffff;
  border-radius: 16px;
  padding: 20px;
  text-align: left;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.25s ease, box-shadow 0.25s ease;
  border: 1px solid #e0e0e0;
  width: 100%;
  max-width: 320px;
}

.location-card:hover {
  transform: translateY(-6px);
  box-shadow: 0 8px 20px rgba(0, 199, 255, 0.25);
  border-color: #00c7ff;
}

.location-name {
  font-size: 1.4rem;
  font-weight: 700;
  color: #1a1a1a;
  margin-bottom: 12px;
  text-align: center;
}

.location-info {
  font-size: 0.95rem;
  color: #333;
  line-height: 1.6;
}

.location-info strong {
  color: #00c7ff;
  font-weight: 600;
}
</style>
