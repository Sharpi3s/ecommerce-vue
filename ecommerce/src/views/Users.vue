<template>

<!-- Fumgerar inte helt felfritt. Användaren man är inne på stannar kvar om man inte trycker på den rosa knappen igen. 
     Det går att ta bort en order men sian laddas om då man får gå in på användaren igen för att se att ordern tagits bort. 
     Detta fungerar lite bättre på sidan där man ser alla ordrar istället  -->



  <div class="container mt-5">
    <div v-if="this.oneUser.admin">
      <h2 class="mb-5">USERS</h2>
      <div  class="d-flex">
        <div class="col-6 userBody">
        
          <div class="tableHeightUser">

            <table class="table">
              <thead>
                <tr>
                  <th scope="col">Name</th>
                  <th scope="col">Email</th>
                  <th scope="col">User id</th>
                </tr>
              </thead>
              <tbody>
                <user-details v-for="user in users" :key="user._id" :user="user" />
              </tbody>
            </table>
            
          </div>
        </div>

        <div class="col-5 mt-3">
          <h4>User Details:</h4>
          <div>
            <user-admin />
          </div>
        </div>

      </div>
    </div>

    <div v-else>
      <not-found />
    </div>

  </div>
</template>

<script>

import {mapActions, mapGetters} from 'vuex'
import NotFound from '../components/Error/NotFound.vue'
import UserAdmin from '../components/User/UserAdmin.vue'
import UserDetails from '../components/User/UserDetails.vue'

export default {
  components: {
    UserDetails,
    UserAdmin,
    NotFound
   
    
  },
  methods: {
    ...mapActions(['getUsers']),

  },
  computed: {
    ...mapGetters(['users', 'oneUser'])
  },
  mounted() {
    this.getUsers()
  }
}
</script>

<style>
  .userBody {
    height: calc(100vh - 420px);
    overflow-y: auto;
    margin-bottom: 2rem;
    margin-right: 5rem;
  }
   .tableHeightUser {
    max-height: calc(100vh - 300px);
    overflow-y: auto;
  }

</style>