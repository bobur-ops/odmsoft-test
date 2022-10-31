<template>
  <div class="container">
    <table>
      <thead>
        <tr>
          <th>
            <input type="checkbox" disabled />
          </th>
          <th @click="$emit('sort', 'first_name')">Name</th>
          <th>Last name</th>
          <th>Email</th>
          <th>IP adress</th>
          <th @click="$emit('sort', 'gender')">Gender</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <td>
            <input type="checkbox" />
          </td>
          <td>{{ user.first_name }}</td>
          <td>{{ user.last_name }}</td>
          <td>{{ user.email }}</td>
          <td>{{ user.ip_address }}</td>
          <td>{{ user.gender }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  props: ["users"],
};
</script>
<style scoped>
th {
  text-align: left;
  padding: 15px 0;
}
td {
  padding: 20px 0;
}
table tbody tr:hover {
  background: #eee3ff;
  cursor: pointer;
  color: #4005a0;
}
thead {
  background: #f5f5f5;
}
th,
td {
  font-weight: 500;
  font-size: 13px;
}
table,
tr {
  border: 1px solid #e1cfff;
}
table {
  border-collapse: collapse;
  width: 100%;
  border-radius: 12px;
  box-shadow: 0px 45px 112px rgba(0, 0, 0, 0.06),
    0px 22.7812px 48.825px rgba(0, 0, 0, 0.0405),
    0px 9px 18.2px rgba(0, 0, 0, 0.03),
    0px 1.96875px 6.475px rgba(0, 0, 0, 0.0195);
}
table,
table thead tr th:first-child {
  overflow: hidden;
  border-top-left-radius: 12px;
}
table thead tr th:first-child,
table tbody tr td:first-child {
  padding-left: 20px;
}
</style>
