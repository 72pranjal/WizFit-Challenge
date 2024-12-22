  <template>
    <div class="container">
      <h1>Are you ready to take the challenge?</h1>
      <div class="download-section">
        <p>Download Harlem Wizards App</p>
        <div class="store-images">
          <img src="/images/apple-store.png" alt="App Store">
          <img src="/images/goolge-store.png" alt="Goolge Store">
        </div>
      </div>
      <input type="text" v-model="searchQuery" placeholder="Search for a school..." @input="onSearchInput" />
      <div class="" v-if="!loading && schools.length">
        <SchoolCard v-for="school in schools" :key="school.id" :schoolData="school" />
      </div>
      <div v-if="loading" class="loading">Loading...</div>
      <div v-if="!loading && schools.length === 0" class="no-results">No schools found for "{{ searchQuery }}"</div>
      <div v-if="error" class="error">{{ error }}</div>
    </div>
  </template>
<script>
import axios from 'axios'
import debounce from 'lodash/debounce';
export default {
  name: 'Search',
  data() {
    return {
      searchQuery: '',
      schools: [],
      loading: false,
      error: null,
    };
  },
  methods: {
    async fetchSchools(isFirstLoad) {
      this.loading = true;
      this.error = null;
      await axios.get(`https://api.devharlemwizardsinabox.com/campaign/campaign_school_list/?search=${this.searchQuery}`)
        .then(response => {
          this.loading = false
          if (isFirstLoad) {
            const lists = response.data.school_list
            this.schools = lists.length > 2 ? lists.slice(0, 2) : lists
          } else {
            this.schools = response.data.school_list
          }
        })
        .catch(error => {
          console.log("API ERROR -----", error)
          this.error = error
        })
    },
    onSearchInput: debounce(function () {
      let check = false
      let input = document.querySelector('input')
      if (input.innerText === '') check = true
      this.fetchSchools(check);
    }, 500),

  },
  mounted() {
    this.fetchSchools(true);
  },
};
</script>

<style scoped>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
  box-shadow: 0 0 10px #ddd;
  background: #fff;
  margin-top: -25px;
  border-radius: 10px;
  min-height: 400px;
}

.container h1 {
  color: brown;
  font-weight: 800;
}

.download-section {
  padding: 25px 0;
}

.download-section p {
  font-size: 17px;
  color: #000;
  font-weight: 700;
}

.download-section .store-images {
  margin-top: 12px;
}

.download-section .store-images img {
  width: 20%;
}

input {
  width: 75%;
  padding: 12px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

input:focus-visible {
  outline: none;
}

.loading,
.no-results,
.error {
  margin: 20px;
  font-size: 1.2em;
}

.error {
  color: red;
}
</style>