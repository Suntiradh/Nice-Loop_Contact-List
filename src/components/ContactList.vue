<template>
  <div class="contact-list">
    <div>
      <h3>Search Contact</h3>
      <input type="text" v-model="searchData" placeholder="Enter Name" />
    </div>
    <br />

    <form @submit.prevent="addContact" class="from-contact">
      <h3>Add Contact</h3>
      <div class="row">
        <div class="column">
          <label>Name</label><br />
          <input style="width: 80%" type="text" v-model="name" required />
        </div>
        <div class="column">
          <label>Phone Number</label><br />
          <input
            type="tel"
            v-model="phoneNum"
            pattern="[0-9]{10}"
            placeholder="0123456789"
            required
          />
        </div>
      </div>

      <div style="margin-top: 30px">
        <label>Email</label><br />
        <input type="email" v-model="email" required />
      </div>
      <div style="margin-top: 30px">
        <button type="submit">Add</button>
      </div>
    </form>
    <br />
    <div class="from-contact" style="text-align: center; margin-top: 50px">
      <p v-if="showCheckData">{{ checkData }}</p>
      <div
        v-for="(info, index) in filteredList"
        :key="info.id"
        style="margin-top: 20px"
      >
        <div v-if="!info.editing">
          <span> <strong>Name :</strong> {{ info.name }} </span><br />
          <span> <strong>Phone Number :</strong> {{ info.phoneNum }} </span
          ><br />
          <span> <strong>E-mail : </strong>{{ info.email }} </span>
        </div>
        <div v-else>
          <div class="row">
            <div class="column" style="text-align: left">
              <label>Name</label>
              <input style="width: 80%" type="text" v-model="info.name" />
            </div>
            <div class="column" style="text-align: left">
              <label>Phone Number</label>
              <input type="tel" v-model="info.phoneNum" pattern="[0-9]{10}" />
            </div>
          </div>
          <div style="margin-top: 30px; text-align: left">
            <label style="text-align: left">Email</label>
            <input type="email" v-model="info.email" />
          </div>
        </div>
        <div style="margin-top: 20px">
          <button
            class="DeleteButton"
            type="button"
            @click="deleteContact(index)"
          >
            Delete
          </button>
          <button class="EditButton" type="button" @click="editContact(info)">
            Edit
          </button>
          <button class="DoneButton" type="button" @click="doneEdit(info)">
            Done
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: 1,
      name: "",
      phoneNum: "",
      email: "",
      data: [],
      searchData: "",
      checkData: "",
      showCheckData: false,
    };
  },
  methods: {
    // Add Contact Data
    addContact() {
      this.data.push({
        name: this.name,
        phoneNum: this.phoneNum,
        id: this.id,
        email: this.email,
        editing: false,
      });
      this.name = "";
      this.phoneNum = "";
      this.email = "";
      this.id++;
    },
    // Delete Contact Data
    deleteContact(index) {
      const newData = [...this.data];
      newData.splice(index, 1);
      this.data = newData;
    },
    // Check Edit
    editContact(info) {
      info.editing = true;
    },
    // Edit Done
    doneEdit(info) {
      info.editing = false;
      this.name = info.name;
      this.phoneNum = info.phoneNum;
      this.email = info.email;
      this.name = "";
      this.phoneNum = "";
      this.email = "";
    },
  },
  // Search Data
  computed: {
    filteredList() {
      return this.data.filter((data) => {
        if (data.name.toLowerCase().includes(this.searchData.toLowerCase())) {
          this.showCheckData = false;
          this.checkData = "";
          return data.name
            .toLowerCase()
            .includes(this.searchData.toLowerCase());
        } else {
          this.checkData = "Not Found";
          this.showCheckData = true;
        }
      });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.contact-list input {
  padding: 8px 15px;
  width: 100%;
}
.column {
  float: left;
  width: 50%;
}
.row:after {
  content: "";
  display: table;
  clear: both;
}
.from-contact {
  text-align: left;
}
button[type="submit"],
button[type="button"] {
  border: 1px solid #dddddd;
  padding: 10px 25px;
  border-radius: 5px;
  background-color: #272eec;
  color: white;
  cursor: pointer;
}
button.DeleteButton {
  background-color: red;
}
button.DoneButton {
  background-color: #4caf50;
}
button.EditButton {
  background-color: #eaa314;
}
</style>
