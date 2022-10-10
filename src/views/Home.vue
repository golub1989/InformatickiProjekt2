<template>
  <div>
     <div>
      <v-data-table
        v-for="item in apiData"
        :key="item"
        :headers="headers"
        :items="item"
        item-key="name"
        class="elevation-1"
        :search="search"
        :custom-filter="filterOnlyCapsText"
      >
      <template >
        <tr>
          <td></td>
          <td>
            <v-text-field
              v-model="calories"
              type="number"
              label="Less than"
            ></v-text-field>
          </td>
          <td colspan="4"></td>
        </tr>
      </template>
    </v-data-table>
  </div>
  </div>
</template>

<script>
export default {
  name: 'HomeView',
  data: () => ({
    apiData: [],
  }),
  methods: {
    async getFromApi() {
      const options = {
        url: "https://free-football-soccer-videos.p.rapidapi.com/",
        headers: {
          'X-RapidAPI-Key': '13c353cee8msh2be1188818bb5f6p12385djsn67fc020f0db3',
          'X-RapidAPI-Host': 'free-football-soccer-videos.p.rapidapi.com',
        },
      }
      await this.axios.request(options).then((response) => {
        this.apiData = []
        this.apiData.push(response.data);
        console.log("apiData 2",this.apiData)
      });
    },
  },
  computed: {
      headers () {
        return [
          {
            text: '',
            align: 'start',
            sortable: false,
            value: 'title',
          },
          {
            text: 'Date',
            value: 'date',
          },
          { text: 'URL',sortable: false, value: 'url' },
        ]
      },
    },
    created() {
      this.getFromApi()
    }
};
</script>

<style>
</style>