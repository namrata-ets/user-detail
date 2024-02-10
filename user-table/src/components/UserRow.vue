<template>
    <tr>
      <td>{{ index + 1 }}</td>
      <td>{{ user.name }}</td>
      <td>{{ user.dob }}</td>
      <td>{{ user.email }}</td>
      <td>{{ user.location }}</td>
      <td>{{ user.phone }}</td>
      <td><img :src="user.picture" alt="User Picture" width="50"></td>
    </tr>
  </template>
  
  <script>
  export default {
    props: {
      user: {
        type: Object,
        required: true
      },
      index: {
        type: Number,
        required: true
      }
    }
  };
  </script>
  