<template>
  <div class="location-card">
    <h3 class="location-name">{{ location.name }}</h3>
    <div class="location-info">
      <p><strong>Tipo:</strong> {{ location.type }}</p>
      <p><strong>Dimensión:</strong> {{ location.dimension }}</p>
      <p><strong>Residentes:</strong> {{ location.residents.length }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'LocationCard',
  props: {
    location: {
      type: Object,
      required: true
    }
  }
}
</script>

<style scoped>
.location-card {
  background: white;
  border-radius: 15px;
  padding: 20px;
  width: 100%;
  max-width: 280px;
  text-align: left;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  transition: transform 0.3s ease;
}

.location-card:hover {
  transform: translateY(-6px);
}

.location-name {
  font-size: 1.2rem;
  font-weight: bold;
  color: #333;
  margin-bottom: 10px;
}

.location-info p {
  margin: 6px 0;
  color: #555;
  font-size: 0.95rem;
}
</style>
