<template>
    <div class="table">
        <h1>Table Data with Axios</h1>
        <h2>{{ result }}</h2>

        <table>
            <caption>Statement Summary</caption>
            <thead>
                <tr>
                    <th scope="col">#SL</th>
                    <th scope="col">Account</th>
                    <th scope="col">Due Date</th>
                    <th scope="col">Amount</th>
                    <th scope="col">Period</th>
                </tr>
            </thead>
            <tbody>
                <Suspense>
                <template #fallback>
                    <div style="text-align:center">loading...</div>
                </template>

                    <SuspenseTableRow />

                </Suspense>
            </tbody>
        </table>    

  </div>
</template>

<script>
import SuspenseTableRow from './SuspenseTableRow.vue'

export default {
    name: "Table",
    components: {
        SuspenseTableRow
    },
    setup() {

    },
}
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
