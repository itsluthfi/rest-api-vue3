<template>
  <div id="spin" :class="spin == 'hide'? 'd-none' : ''" class="position-absolute position-absolute top-50 start-50 translate-middle  w-100 h-100 opacity-50" style="background-color: #fff; z-index: 5;">
    <div class="spinner-border text-primary position-absolute top-50 start-50" style="width: 5rem; height: 5rem;" role="status">
      <span class="visually-hidden">Loading...</span>
    </div>
  </div>
 
  <div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-8">
      

        <div class="d-flex justify-content-between">
          <router-link
          :to="{ name: 'transaction.create' }"
          class="btn btn-primary btn-sm rounded shadow mb-3"
          >Add</router-link
        >
        <button @click="[destroy('all',false),spin = 'show']" class="btn btn-danger btn-sm rounded shadow mb-3">Delete All</button>
        </div>

        <div class="card rounded shadow">
          <div class="card-header">Transaction List</div>
          <div class="card-body">
            <table class="table">
              <thead>
                <tr>
                  <th>Title</th>
                  <th>Amount</th>
                  <th>Type</th>
                  <th>Action</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(transaction, index) in transactions.data"
                  :key="index"
                >
                  <td>{{ transaction.title }}</td>
                  <td>{{ transaction.amount }}</td>
                  <td>{{ transaction.type }}</td>
                  <td>
                    <router-link
                      :to="{
                        name: 'transaction.edit',
                        params: { id: transaction.id },
                      }"
                      class="btn btn-sm btn-outline-info"
                      >Edit</router-link
                    >
                    <button
                      class="btn btn-sm btn-outline-danger"
                      @click.prevent="[destroy(transaction.id,index),spin = 'show']"
                    >
                      Delete
                    </button>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { onMounted,ref } from "vue";
export default {
  setup() {
    // reactive state
    let spin = ref('show');
    let transactions = ref([]);
    onMounted( () =>{
      // get data from api endpoint
      axios
        .get("http://localhost:8000/api/transaction")
        .then((result) => {
          transactions.value = result.data;
          spin.value = 'hide';
          
        })
        .catch((err) => {
          console.log(err);
        });
    });

    function destroy(id,index) {
      axios
        .delete(`http://localhost:8000/api/transaction/${id}`, transactions)
        .then( () =>  {
          spin.value = 'hide';
          index  ?  transactions.value.data.splice(index, 1) : transactions.value.data = [];
        })
        .catch((err) => {
          console.log(err.response.data);
        });
    }

    return {
      transactions,
      destroy,
      spin
    };
  },
};
</script>

<style></style>
