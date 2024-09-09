<template>
  <div class="container">
    <div class="center">Current Spotify Song</div>
  </div>
</template>

<script>
export default {
  name: 'HomePage',
  data() {
    return {
      token: 'BQB_M2Ae63naDAOlkFHKpidZHf7R0QnagtRpClRjBmvBmGbKHjYv6A_Mib8kChDU7rFS8D0r9rX6lkOxxoCoRq6rYT21oCB1wF6lJ_K1hMkjRBNC1zzL6SRHfRRu1F0ckyghHGimLBUpwkBpcaR-XkAz2qbV8S4X6_fY6GyIZjbDqQvbKJgDkbZ0Y_BE80O_IvU8aFRxrJ0A-kvfSCsKQbzvMCXNW9wwlYZf5WFR8vQKYfR0xoorqbZpLx7Wy2BGxGhqZIKFmAtbZK8ydF84CfnTNn2bcZU2'
    }
  },
  async mounted() {
    try {
      const data = await this.fetchWebApi('v1/me/top/tracks?time_range=long_term&limit=5', 'GET');
      console.log(data.items);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  },
  methods: {
    async fetchWebApi(endpoint, method, body) {
      const res = await fetch(`https://api.spotify.com/${endpoint}`, {
        headers: {
          Authorization: `Bearer ${this.token}`,
          'Content-Type': 'application/json'
        },
        method,
        body: body ? JSON.stringify(body) : undefined
      });

      if (!res.ok) {
        throw new Error(`HTTP error! status: ${res.status}`);
      }

      return await res.json();
    }
  },
}
</script>


<style scoped>

.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.center {
  background-color: yellow;
}
</style>
