<template>
  <div class="container my-5">
    <div class="row justify-content-center">
      <div class="col-8">
        <router-link
          :to="{ name: 'transaction.create' }"
          class="btn btn-primary btn-sm rounded shadow mb-3"
          >Add</router-link
        >

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
                <tr>
                  <td>Income</td>
                  <td>500000</td>
                  <td>Revenue</td>
                  <td>
                    <router-link
                      :to="{ name: 'transaction.edit', params: { id: 1 } }"
                      class="btn btn-sm btn-outline-info"
                      >Edit</router-link
                    >
                    <button class="btn btn-sm btn-outline-danger">
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
export default {};
</script>

<style></style>
