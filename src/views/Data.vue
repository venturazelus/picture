<template>
<div>
    <base-header class="pb-6 pb-8 pt-5 pt-md-8 bg-gradient-success">
      <!-- Card stats -->
      <b-row>
        <b-col xl="3" md="6">
          <stats-card title="Total traffic"
                      type="gradient-red"
                      sub-title="350,897"
                      icon="ni ni-active-40"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">3.48%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Total traffic"
                      type="gradient-orange"
                      sub-title="2,356"
                      icon="ni ni-chart-pie-35"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">12.18%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Sales"
                      type="gradient-green"
                      sub-title="924"
                      icon="ni ni-money-coins"
                      class="mb-4">

            <template slot="footer">
              <span class="text-danger mr-2">5.72%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>

        </b-col>
        <b-col xl="3" md="6">
          <stats-card title="Performance"
                      type="gradient-info"
                      sub-title="49,65%"
                      icon="ni ni-chart-bar-32"
                      class="mb-4">

            <template slot="footer">
              <span class="text-success mr-2">54.8%</span>
              <span class="text-nowrap">Since last month</span>
            </template>
          </stats-card>
        </b-col>
      </b-row>
    </base-header>

    <div id="app">
         <div class="container">
            <div>
               <b-form @submit="onSubmit" @reset="onReset" v-if="show">
                     <b-form-group
                     id="input-group-1"
                     label="Id:"
                     label-for="input-1"
                     >
                     <b-form-input
                        id="input-1"
                        v-model="form.id"
                        type="text"
                        @keypress="IsNumber($event)"
                        required
                        placeholder=""
                     >
                     </b-form-input>
                     </b-form-group>

                     <b-form-group
                     id="input-group-2"
                     label="First Name:"
                     label-for="input-2"
                     >
                     <b-form-input
                        id="input-2"
                        v-model="form.first_name"
                        type="text"
                        @keypress="IsLetter($event)"
                        required
                        placeholder=""
                     >
                     </b-form-input>
                     </b-form-group>

                     <b-form-group
                     id="input-group-3"
                     label="Last Name:"
                     label-for="input-3"
                     >
                     <b-form-input
                        id="input-3"
                        v-model="form.last_name"
                        type="text"
                        @keypress="IsLetter($event)"
                        required
                        placeholder=""
                     >
                     </b-form-input>
                     </b-form-group>

                     <b-form-group
                     id="input-group-4"
                     label="Email:"
                     label-for="input-4"
                     >
                     <b-form-input
                        id="input-4"
                        v-model="form.email"
                        type="email"
                        required
                        placeholder=""
                     >
                     </b-form-input>
                     </b-form-group>

                     <b-button  @click="showMsgBoxTwo" type="submit" variant="primary">Submit</b-button>
                     <b-button type="reset" variant="danger">Reset</b-button>
                  </b-form>


                  <b-table
                     id="my-table"
                     :items="items"
                     :fields="fields"
                     :per-page="perPage"
                     :current-page="currentPage"
                     striped hover
                  >
                  </b-table>
                  <b-pagination
                     v-model="currentPage"
                     :total-rows="rows"
                     :per-page="perPage"
                     aria-controls="my-table"
                  >
                  </b-pagination>
             </div>
         </div>
      </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        boxTwo: '',
        perPage: 5,
        currentPage: 1,
        fields: [
          {
            key: "id",
            sortable: true
          },
          {
            key: "first_name",
          },
          {
            key: "last_name",
          },
          {
            key: "email",
          }
        ],
        items: [
        ],
        form: {
          id: '',
          first_name: '',
          last_name: '',
          email: '',
        },
        show: true,
      }
    },
    computed: {
      rows() {
        return this.items.length
      }
    },
    methods: {
      onSubmit(evt) {
        evt.preventDefault()
        this.items.push({ id: this.form.id, first_name: this.form.first_name, last_name: this.form.last_name, email : this.form.email, })
      },
      onReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.form.id = ''
        this.form.first_name = ''
        this.form.last_name = ''
        this.form.email = ''
        this.form_action = 'Insert'
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },
      IsNumber(event) {
       if (!/\d/.test(event.key) && event.key !== '.') return event.preventDefault();
      },
      IsLetter(e) {
      let char = String.fromCharCode(e.keyCode);
      if(/^[A-Za-z ]+$/.test(char)) return true; 
      else e.preventDefault(); 
      },
      validEmail: function (email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
     },
      showMsgBoxTwo() {
        this.boxTwo = ''
        this.$bvModal.msgBoxOk('Data was submitted successfully', {
          title: 'Confirmation',
          size: 'sm',
          buttonSize: 'sm',
          okVariant: 'success',
          headerClass: 'p-2 border-bottom-0',
          footerClass: 'p-2 border-top-0',
          centered: true
        })
          .then(value => {
            this.boxTwo = value
          })
          .catch(err => {
            // An error occurred
          })
      }
    },
  }
</script>