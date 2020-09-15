<template>
  <div class="container">
    <div class="phone-list-grid1">
      <span>
        <strong>............. Phone List</strong>
      </span>
    </div>
    <div class="phone-list-grid2">
      <div class="phone-list-grid4">
        <input v-model="saveName" class="phone-list-text-box" placeholder="Name *" />
        <input v-model="saveSurname" class="phone-list-text-box" placeholder="Surname *" />
        <input v-model="savePhone" class="phone-list-text-box"  placeholder="Phone Number *" />
        <input v-model="saveEmail" class="phone-list-text-box"   placeholder="E-mail *" />
        <input v-model="saveCompany" class="phone-list-text-box"   placeholder="Company *" />
        <button @click="personSave()" id="saveButton">Save</button>
      </div>
      <div class="phone-list-grid5">
        <div class="phone-list-search">
          <input class="phone-list-text-box" type="text" v-model="search" placeholder="Searh"/>
        </div>
        <div class="phone-list-list-name">
          <div class="phone-list-name-bar">
            <strong>Name</strong>
          </div>
          <div class="phone-list-name-bar">
            <strong>Surname</strong>
          </div>
          <div class="phone-list-name-bar">
            <strong>Phone</strong>
          </div>
          <div class="phone-list-name-bar">
            <strong>E-mail</strong>
          </div>
          <div class="phone-list-name-bar">
            <strong>Company</strong>
          </div>
          <div class="phone-list-name-bar">
            <strong>Delete</strong>
          </div>
        </div>
        <div class="phone-list-list-content" v-for="(personal , index ) in current" :key="index">
          <div class="phone-list-list-persons-content">{{ personal.name }}</div>
          <div class="phone-list-list-persons-content">{{ personal.surname }}</div>
          <div class="phone-list-list-persons-content">{{ personal.phone }}</div>
          <div class="phone-list-list-persons-content">{{ personal.email }}</div>
          <div class="phone-list-list-persons-content">{{ personal.company }}</div>
          <div class="phone-list-list-persons-content">
            <button @click="deletePerson(index)" id="removeButton">Delete</button>
            <button @click="editPerson(index)" id="editButton">Edit</button>
          </div>
        </div>
        <div class="prev-next-button-bar" v-if="pageCounter != 0">
          <div>
            <button
              class="prev-next-button"
              @click="pageNumber = pageNumber -1"
              :disabled="pageNumber == 0"
            >Previous Page</button>
            <span>{{ pageNumber + 1 }} OF {{ pageCounter + 1 }}</span>
            <button
              class="prev-next-button"
              @click="pageNumber = pageNumber +1"
              :disabled="pageNumber == pageCounter"
            >Next Page</button>
          </div>
        </div>
      </div>
    </div>
    <div class="phone-list-grid3">
      <strong>This page was created by <a href="https://twitter.com/yahyadereli">Yahya Dereli</a></strong>
    </div>
  </div>
</template>
<script>
export default {
  data: () => {
    return {
      personsList: [],
      saveName: "",
      saveSurname: "",
      savePhone: "",
      saveEmail: "",
      saveCompany: "",
      pageNumber: 0,
      perPage: 25,
      search:""
    };
  },
  computed: {
    current() {
      if(this.search !=""){
        return this.personsList.filter(personal => {
        return personal.name.toLowerCase().includes(this.search.toLowerCase()) ||
               personal.surname.toLowerCase().includes(this.search.toLowerCase()) ||
               personal.phone.toLowerCase().includes(this.search.toLowerCase()) ||
               personal.email.toLowerCase().includes(this.search.toLowerCase()) ||
               personal.company.toLowerCase().includes(this.search.toLowerCase())
      });
      }else{
        return this.personsList.slice(
        this.pageNumber * this.perPage,
        this.pageNumber * this.perPage + this.perPage);
      }
    },
    pageCounter() {
      let l = this.personsList.length,
        s = this.perPage;
      return Math.floor(l / s);
    }
  },
  methods: {
    personSave() {
      if (
        this.saveName == "" ||
        this.saveSurname == "" ||
        this.savePhone == "" ||
        this.saveEmail == "" ||
        this.saveCompany == ""
      ) {
        window.alert("Marked fields cannot be left blank");
      } else {
        const person = { name: "", surname: "", phone: "" , email: "" ,company: ""};
        person.name = this.saveName;
        person.surname = this.saveSurname;
        person.phone = this.savePhone;
        person.email = this.saveEmail
        person.company = this.saveCompany
        this.personsList.push(person);
        this.saveName = "";
        this.saveSurname = "";
        this.savePhone = "";
        this.saveEmail = "";
        this.saveCompany = "";
      }
    },
    deletePerson(index) {
      if(confirm("Registration will be deleted, do you confirm?")){}
      else{ return false; }
      this.personsList.splice(index, 1);
    },
    editPerson(index) {
      const person = this.personsList[index]
       this.saveName = person.name;
       this.saveSurname = person.surname;
       this.savePhone = person.phone;
       this.saveEmail = person.email;
       this.saveCompany = person.company;
      this.personsList.splice(index, 1);
    }
  }
};
</script>

<style>
.container {
  display: grid;
  width: 100%;
  height: 98vh;
  max-height: 1000px;
  margin: auto;
  grid-template-rows: 1fr 20fr 0.5fr;
  grid-gap: 10px;
  background-color: rgb(214, 223, 241);
}
.phone-list-grid1 {
  text-align: center;
}
.phone-list-grid2 {
  display: grid;
  grid-template-columns: 1fr 10fr;
  grid-gap: 10px;
}
.phone-list-grid3 {
  background-color: rgb(255, 231, 231);
  text-align: center;
}
.phone-list-grid4 {
  display: flex;
  flex-direction: column;
  justify-content: baseline;
  align-items: flex-end;
  padding: 10px;
}
.phone-list-grid5 {
  background-color: rgb(181, 181, 185);
  padding: 10px;
}
.phone-list-search {
  text-align: right;
}
.phone-list-text-box {
  height: 30px;
  margin-right: 10px;
  margin-bottom: 10px;
  border: 1px solid #666;
}
.phone-list-list-name {
  display: flex;
  flex-direction: row;
  display: grid;
  grid-template-columns: 3fr 3fr 3fr 3fr 3fr 1fr;
  background-color: rgb(148, 148, 170);
}
.phone-list-list-content {
  display: flex;
  flex-direction: row;
  display: grid;
  grid-template-columns: 3fr 3fr 3fr 3fr 3fr 1fr;
  text-align: center;
  margin: 2px;
  font-size: 20px;
}
.phone-list-name-bar {
  text-align: center;
  font-size: 20px;
}
.phone-list-list-persons-content {
  border: 0.5px solid #666;
}
#saveButton {
  background-color: rgb(83, 122, 83);
  border: 1px solid green;
  border-radius: 5px;
}
#removeButton {
  background-color: rgb(175, 17, 30);
  border: 1px solid red;
  border-radius: 5px;
  color: aliceblue;
}
#editButton {
  background-color: rgb(0, 189, 0);
  border: 1px solid green;
  border-radius: 5px;
  color: aliceblue
}
.prev-next-button {
  border: 1px solid #0066cc;
  background-color: #0099cc;
}
.prev-next-button-bar {
  display: flex;
  justify-content: center;
}
.prev-next-button:disabled,
.prev-next-button[disabled] {
  border: 1px solid #999999;
  background-color: #cccccc;
}
</style>
