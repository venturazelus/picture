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


    <b-row class="justify-content-center my-4">
    <b-button v-b-modal.modal-prevent-closing >Tambah Data</b-button>
    </b-row>

    <div class="mt-3">
     <b-table class="ma-5 "
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

    <b-modal
      id="modal-prevent-closing"
      ref="modal"
      title="Submit Your data"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
    <form ref="form" @submit.stop.prevent="handleSubmit">
        <b-form-group
          label="ID"
          label-for="id-input"
          invalid-feedback="ID is required"
          :state="idState"
        >
          <b-form-input
            id="id-input"
            v-model="id"
            :state="idState"
            type = "text"
            @keypress="IsNumber($event)"
            required
          >
          </b-form-input>
        </b-form-group>

        <b-form-group
          label="Name"
          label-for="name-input"
          invalid-feedback="Name is required"
          :state="nameState"
        >
          <b-form-input
            id="name-input"
            v-model="name"
            :state="nameState"
            type = "text"
            @keypress="IsLetter($event)"
            required
          >
          </b-form-input>
        </b-form-group>

        <b-form-group
          label="Email"
          label-for="email-input"
          invalid-feedback="Email is required"
          :state="emailState"
        >
          <b-form-input
            id="email-input"
            @keypress="IsEmail($event)"
            v-model="email"
            :state="emailState"
            type = "email"
            required
          ></b-form-input>
        </b-form-group>
      </form>
    </b-modal>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        perPage: 5,
        currentPage: 1,
        id : '',
        name: '',
        email : '',
        idState : null,
        nameState: null,
        emailState : null,
        submittediId : [],
        submittedNames: [],
        submittedEmails : [],
        fields: [
          {
            id : "id",
          },  
          {
            key: "name",
          },
          {
            key: "email",
          },
        ],
        items : []
      }
    },
    computed: {
      rows() {
        return this.items.length
      }
    },
    methods: {
      checkFormValidity() {
        const valid = this.$refs.form.checkValidity()
        this.idState = valid
        this.nameState = valid
        this.emailState = valid
        return valid
      },
      resetModal() {
        this.id = ''
        this.idState = null
        this.name = ''
        this.nameState = null
        this.email = ''
        this.emailState = null
      },
      handleOk(bvModalEvt) {
        bvModalEvt.preventDefault()
        this.handleSubmit()
      },
      handleSubmit() {
        if (!this.checkFormValidity()) {
          return
        }
        this.items.push({id : this.id, name : this.name, email : this.email})
        this.$nextTick(() => {
          this.$bvModal.hide('modal-prevent-closing')
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
    }
  }
</script>