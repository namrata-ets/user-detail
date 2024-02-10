<template>
  <table border="1">
    <thead>
      <tr>
        <th v-for="col in columns" :key="col" @click="sortBy(col)">
          {{ col }}
          <span v-if="sortKey === col" :class="sortOrders[col] > 0 ? 'arrow-up' : 'arrow-down'"></span>
        </th>
      </tr>
    </thead>
    <tbody>
      <user-row v-for="(user, index) in sortedUsers" :key="user.email" :user="user" :index="index"></user-row>
    </tbody>
  </table>
</template>

<script>
import UserRow from './UserRow.vue';

export default {
  components: {
    UserRow
  },
  props: {
    users: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      columns: ['slno.', 'name', 'DOB', 'Email', 'Location', 'Phone', 'Picture'],
      sortKey: '',
      sortOrders: {}
    };
  },
  mounted() {
    // Set initial sort order to descending for all columns
    this.columns.forEach(col => {
      this.sortOrders[col] = -1;
    });
    // Set initial sort key to first column
    this.sortKey = this.columns[0];
  },
  methods: {
    sortBy(key) {
      this.sortKey = key;
      this.sortOrders[key] = this.sortOrders[key] * -1;
    }
  },
  computed: {
    sortedUsers() {
      const key = this.sortKey;
      const order = this.sortOrders[key] || 1;
      return this.users.slice().sort((a, b) => {
        a = typeof a[key] === 'string' ? a[key].toLowerCase() : a[key];
        b = typeof b[key] === 'string' ? b[key].toLowerCase() : b[key];
        return order * (a > b ? 1 : -1);
      });
    }
  }
};
</script>
