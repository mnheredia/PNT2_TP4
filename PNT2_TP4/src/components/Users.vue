<template lang="html">
  <section class="src-components-users">
    <div class="jumbotron jumbotron-fluid">
      <button class="btn btn-outline-primary my-3 mr-3" @click="XHR">
        XHR
      </button>
      <button class="btn btn-outline-secondary" @click="FETCH">
        Fetch
      </button>
      <button class="btn btn-outline-info" @click="AXIOS">
        AXIOS
      </button>
      <div v-if="users.length" class="table-responsive">
        <table class="table active">
          <tr style="font-size: 32px; font-weight: lighter; font-style: italic;" >
            <th v-for="(col, i) in getColumnas" :key="i">{{ col }}</th>
          </tr>
          <tr v-for="(user, i) in users" :key="i">
            <td v-for="(col, i) in getColumnas" :key="i">{{ user[col] }}</td>
          </tr>
        </table>
      </div>
    </div>
  </section>
</template>
 
<script lang="js">
export default {
  name: 'src-components-users',
  props: [],
  mounted() {
  },
  data() {
    return {
      url: 'https://60beb3776035840017c17899.mockapi.io/users',
      users: []
    }
  },
  methods: {
    XHR() {
      let xhr = new XMLHttpRequest();
      xhr.open('GET', this.url)
      xhr.addEventListener('load', () => {
        if(xhr.status !== 200) console.error(`error get ${status}`);
        const { response } = xhr;
        const parsed = JSON.parse(response);
        this.users = parsed;
      });
      xhr.addEventListener('error', e => console.error(`error en xhr: ${e}`))
      xhr.send();
    },
    FETCH() {
      fetch(this.url)
          .then(d => d.json())
          .then(r => { this.users = r })
          .catch(e => console.error(e))
    },
    AXIOS() {
      this.axios(this.url)
          .then(r => {
            this.users = r.data
          })
          .catch(e => console.error(e))
    }
  },
  computed: {
    getColumnas() {
      return Object.keys(this.users[0])
    }
  }
}
</script>
