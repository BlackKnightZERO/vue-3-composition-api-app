<template>
    <template v-if="requestError">
      <tr><td colspan="5">{{ requestError }}</td></tr>
    </template>
    <template v-else>
      <tr v-for="(row, index) in data" :key="index">
          <td data-label="index">{{ ++index }}</td>
          <td data-label="Account">{{ row.account }}</td>
          <td data-label="Due Date">{{ row.due_date }}</td>
          <td data-label="Amount">{{ row.amount }}</td>
          <td data-label="Period">{{ row.period }}</td>
      </tr>
    </template>
</template>

<script>
import { ref, defineComponent } from "vue";
import axios from 'axios'

export default defineComponent({
    async setup() {
        const data = ref(null)
        const requestError = ref(null)

        const url = `http://localhost:3000/statement`

        await axios.get(url)
        .then(function (response) {
            data.value = response.data
        })
        .catch(function (error) {
              if (error.response) {
                requestError.value = error.message
              } else if (error.request) {
                requestError.value = error.message
              } else {
                requestError.value = error.message
              }
        })

        return { data, requestError }             
    },
})
</script>

<style scoped>
table {
  border: 1px solid #ccc;
  border-collapse: collapse;
  margin: 0 auto;
  padding: 0;
  width: 70%;
  table-layout: fixed;
}

table caption {
  font-size: 1.5em;
  margin: .5em 0 .75em;
}

table tr {
  background-color: #f8f8f8;
  border: 1px solid #ddd;
  padding: .35em;
}

table th,
table td {
  padding: .625em;
  text-align: center;
}

table th {
  font-size: .85em;
  letter-spacing: .1em;
  text-transform: uppercase;
}

@media screen and (max-width: 600px) {
  table {
    border: 0;
  }

  table caption {
    font-size: 1.3em;
  }
  
  table thead {
    border: none;
    clip: rect(0 0 0 0);
    height: 1px;
    margin: -1px;
    overflow: hidden;
    padding: 0;
    position: absolute;
    width: 1px;
  }
  
  table tr {
    border-bottom: 3px solid #ddd;
    display: block;
    margin-bottom: .625em;
  }
  
  table td {
    border-bottom: 1px solid #ddd;
    display: block;
    font-size: .8em;
    text-align: right;
  }
  
  table td::before {
    content: attr(data-label);
    float: left;
    font-weight: bold;
    text-transform: uppercase;
  }
  
  table td:last-child {
    border-bottom: 0;
  }
}
</style>