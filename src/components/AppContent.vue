<script>
import axios from 'axios'
export default {
  data() {
    return {
      projects: [],
      currentPage: 1,
      lastPage: null
    }
  },
  methods: {
    changePage(n) {
      if(n === this.currentPage) return
      this.currentPage = n
      this.fetchProjects()
    },
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
        <div class="h-100">
          <div class="col-auto text-center">
            <h1>My projects:</h1>
          </div>
          <div class="">
            <ul class="row row-cols-1 row-cols-md-2 g-4">
              <li class="col" v-for="project in projects" key="project.id">
                <div class="card">
                  <h3 class="card-header">{{ project.title }}</h3>
                  <div class="card-body card-text">
                    <p>{{ project.description }}</p>
                    <a :href="`${project.project_link}`">{{ project.project_link }}</a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
          <div>
            <ul class="text-center">
              <button class="btn btn-primary m-3 col-2" @click="changePage(n)" v-for="n in lastPage" :key="n">{{ n }}</button>
            </ul>
          </div>
        </div>
      </div>
    </section>
  </main>

</template>

<style></style>