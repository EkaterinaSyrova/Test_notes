<script setup>
defineProps(['cat','dog','pic'])
</script>
<template>
  <div id="app">
    <table>
      <tr>
        <td>
          {{ cat }}
        </td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {

}
</script>


<style lang="scss" scoped>
input {
  width: 400px;
}
img{
  width: 50px;
}
tr{
  height: 100px;
  border: 1px solid black;
}
table{
  border: 1px solid black;
}
td{
  width: 400px;
  border: 1px solid black;
  text-align: center;
  vertical-align: top;
}
textarea{
  width: 400px;
  height: 100px;
}
.remove{
  margin-left: auto;
  margin-right: 0;
}
.form-fields {
  margin-right: 50px;
  margin-bottom: 50px;
}
</style>
