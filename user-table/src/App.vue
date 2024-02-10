<template>
  <div>
    <UserTable :users="users"></UserTable>
  </div>
</template>

<script>
import UserTable from './components/UserTable.vue';

export default {
  components: {
    UserTable
  },
  data() {
    return {
      users: []
    };
  },
  mounted() {
    this.fetchUsers();
  },
  methods: {
    fetchUsers() {
      fetch('https://randomuser.me/api/?results=50')
        .then(response => response.json())
        .then(data => {
          this.users = data.results.map(user => ({
            name: user.name.first + ' ' + user.name.last,
            dob: user.dob.date,
            email: user.email,
            location: `${user.location.street.number} ${user.location.street.name}, ${user.location.city}, ${user.location.state}, ${user.location.country}`,
            phone: user.phone,
            picture: user.picture.medium
          }));
        })
        .catch(error => console.error('Error fetching users:', error));
    }
  }
};
</script>
