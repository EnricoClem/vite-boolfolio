<script>
import axios from 'axios'
export default {
  data() {
    return {
      projects: []
    }
  },
  methods: {
    fetchProjects() {
      axios.get('http://127.0.0.1:8000/api/projects',{
        params: {
          page: this.currentPage,
          perPage: 6
        }
      })
      .then(res => {
        this.projects = res.data.results.data
        this.lastPage = res.data.results.last_page
      })
    }
  },
  created() {
    this.fetchProjects()
  }
}

</script>

<template>

  <main>
    <section class="h-100">
      <div class="container py-5 h-100">
        <div class="row aling-items-center flex-column h-100">
          <div class="col-auto text-center">
            <h1>My projects:</h1>
          </div>
          <div class="col-auto text-center">
            <ul>
              <li v-for="project in projects" key="project.id">
                <h3>{{ project.title }}</h3>
                <p>{{ project.description }}</p>
                <a :href="`{{ project.project_link }}`"></a>
              </li>
            </ul>
          </div>
          <div>
            <ul>
              <li v-for="n in lastPage" :key="n">
                {{ n }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>
  </main>

</template>

<style></style>