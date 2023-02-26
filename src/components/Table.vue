<template>
    <table>
        <thead>
            <tr>
                <th>E<sub>c</sub></th>
                <th>V<sub>b</sub></th>
                <th>z</th>
                <th v-for="(col, index) in cols" :key="index">x<sub>{{ index+1 }}</sub></th>
            </tr>
        </thead>
        <tbody>
            <!-- <tr v-for="(row, index) in rows" :key="index"> -->
            <tr v-for="(row, index) in rows" :key="index">
                <td>{{ index }}</td>
                <td>z</td>
                <td>1</td>
                <!-- <td><frac>1<sub>2</sub></frac></td> -->
                <td><span>1</span>/<sub>2</sub></td>
                <td><sup>5</sup>&frasl;<sub>9</sub></td>
                <td>1<sup>1</sup>&frasl;<sub>2</sub></td>
                <td><sup>(2M-1)</sup>&frasl;<sub>5</sub></td>
                <td>1</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    name: 'SimplexTable',
    props: {
        rows: Number,
        cols: Number
    }
}
</script>

<style scoped>
table {
    border-collapse: collapse;
    width: 100%;
    max-width: 800px;
    margin: 0 auto;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  }
  
  thead th {
    background-color: #f2f2f2;
    font-weight: bold;
    text-align: center;
    padding: 15px;
  }
  
  tbody td {
    border-bottom: 1px solid #ddd;
    padding: 10px;
  }
  
  tbody td:not(:last-child) {
    border-right: 1px solid #ddd;
  }
  
  tbody tr:last-child td {
    border-bottom: none;
  }
  
  tbody tr td:hover {
    background-color: #f5f5f5;
  }
</style>