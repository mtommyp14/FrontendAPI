<template>
  <div class="settings">
    <div class="row">
      <Navbar />
      <div class="col-11 col-sm-11 col-md-11 col-lg-11 col-xl-11 px-0">
        <header>
          <div class="">
            <div class="header ">
              <h1>Setting</h1>
            </div>
          </div>
        </header>
        <div class="tableprod product mt-3 ml-3 col-11">
          <div class="overflow-auto">
            <h4 class="pt-2 pb-2 float-left">Table Product</h4>
            <button class="btn btn-primary mt-2 float-right" v-b-modal.modal-addproduct>Add Product</button>
            <b-table id="my-table" :fields="fields" :items="setproduct" :per-page="perPageProduct"
              :current-page="currentPageProduct" responsive="sm">
              <template #cell(action)="data">
                <b-button @click="editProduct(data.item)" v-b-modal.modal-updateproduct variant="primary mr-2">
                  <b-icon icon="gear"></b-icon>
                </b-button>
                <b-button  variant="danger" @click="onDeleteProduct(data.item.id)">
                  <b-icon icon="trash"></b-icon>
                </b-button>
              </template>
            </b-table>
            <b-pagination v-model="currentPageProduct" :total-rows="rowsproduct" :per-page="perPageProduct"
              aria-controls="my-table" align="center">
            </b-pagination>
          </div>
        </div>
        <div class="addprod">
          <b-modal id="modal-addproduct" hide-footer title="BootstrapVue">
            <b-form @submit="onSubmitAdd" @reset="onResetProduct">
              <b-form-group label="Name:" label-for="name">
                <b-form-input v-model="formadd.name" required placeholder="Product Name">
                </b-form-input>
              </b-form-group>

              <b-form-group label="Price:" label-for="price">
                <b-form-input v-model="formadd.price" required placeholder="Enter Price"></b-form-input>
              </b-form-group>

              <b-form-group label="Image:" label-for="image">
                <b-form-file v-model="formadd.image" required placeholder="Enter Image"></b-form-file>
              </b-form-group>
              <b-form-group label="Category:" label-for="idcategory">
                <b-form-select v-model="formadd.idcategory" :options="category">
                </b-form-select>
              </b-form-group>
              <b-button type="submit" variant="primary">Submit</b-button>
              <b-button class="ml-2" type="reset" variant="danger">Reset</b-button>
            </b-form>
          </b-modal>
        </div>
        <div class="editprod">
          <b-modal id="modal-updateproduct" title="Update Product" hide-footer>
            <b-form>
              <b-form-group id="input-group-2" label="Product Name:" label-for="input-2">
                <b-form-input id="input-2" v-model="formeditproduct.name" placeholder="Enter name product" required>
                </b-form-input>
              </b-form-group>

              <b-form-group id="input-group-4" label="Price:" label-for="input-4">
                <b-form-input id="input-4" v-model="formeditproduct.price" placeholder="Enter price" required>
                </b-form-input>
              </b-form-group>

              <b-form-group id="input-group-5" label="Image:" label-for="input-5">
                <b-form-file id="input-5" v-model="formeditproduct.image" placeholder="Enter Image" required>
                </b-form-file>
              </b-form-group>

              <b-form-group id="input-group-3" label="Type:" label-for="input-3">
                <b-form-select id="input-3" v-model="formeditproduct.type" :options="types" required></b-form-select>
              </b-form-group>
              <b-button type="submit" @click="updateProduct" variant="primary mr-2">Update</b-button>
              <b-button type="reset" @reset="onResetProduct" variant="danger">Reset</b-button>
            </b-form>
          </b-modal>
        </div>

        



        <div class="bottom mt-3 ml-3 row">
          <div class="user mt-1 col-5">
            <div class="overflow-auto">
              <h4 class="pt-2 pb-2 float-left">Table Category</h4>
              <button class="btn btn-primary mt-2 float-right" v-b-modal.modal-addCategory>Add Category</button>
              <b-table id="my-tableCategory" :fields="fieldsCategory" :items="setCategory" :per-page="perPageCategory"
                :current-page="currentPageCategory" responsive="sm">
                <template #cell(action)="dataCategory">
                  <b-button @click="editCategory(dataCategory.item)" v-b-modal.modal-updateCategory variant="primary mr-2">
                    <b-icon icon="gear"></b-icon>
                  </b-button>
                  <b-button v-b-modal.modal-deleteCategory variant="danger" >
                    <b-icon icon="trash"></b-icon>
                  </b-button>
                </template>
              </b-table>
              <b-pagination v-model="currentPageCategory" :total-rows="rowsCategory" :per-page="perPageCategory"
                aria-controls="my-tableCategory" align="center">
              </b-pagination>
            </div>
          </div>




          <div class="category mt-1 col-6 ml-1">
            <div class="overflow-auto">
              <h4 class="pt-2 pb-2 float-left">Table Users</h4>
              <button class="btn btn-primary mt-2 float-right" v-b-modal.modal-addUser>Add Users</button>
              <b-table id="my-tableUser" :fields="fieldsUser" :items="setUser" :per-page="perPageUser"
                :current-page="currentPageUser" responsive="sm">
                <template #cell(action)="dataUser">
                  <b-button @click="editUser(dataUser.item)" v-b-modal.modal-updateUser variant="primary mr-2">
                    <b-icon icon="gear"></b-icon>
                  </b-button>
                  <b-button  variant="danger" @click="onDeleteUser(dataUser.item.id)">
                    <b-icon icon="trash"></b-icon>
                  </b-button>
                </template>
              </b-table>
              <b-pagination v-model="currentPageUser" :total-rows="rowsUser" :per-page="perPageUser"
                aria-controls="my-tableUser" align="center">
              </b-pagination>
            </div>

            <div>
              <b-modal id="modal-addUser" hide-footer title="SignUp">
                <template>
                  <b-form @submit.prevent="onSubmitSignup" @reset="onResetUser">
                    <b-form-group id="input-group-1" label="Email address:" label-for="input-1">
                      <b-form-input id="input-1" v-model="formSignup.email" type="email" placeholder="Enter email"
                        required></b-form-input>
                    </b-form-group>

                    <b-form-group id="input-group-2" label="Your Password:" label-for="input-2">
                      <b-form-input id="input-2" v-model="formSignup.password" placeholder="Enter password" required>
                      </b-form-input>
                    </b-form-group>

                    <b-form-group id="input-group-3" label="Your Name:" label-for="input-3">
                      <b-form-input id="input-3" v-model="formSignup.name" placeholder="Enter name" required>
                      </b-form-input>
                    </b-form-group>
                    <b-button type="submit" variant="primary mr-2 mt-2">Submit</b-button>
                    <b-button type="reset" variant="danger mt-2">Reset</b-button>
                  </b-form>
                </template>
              </b-modal>
            </div>
            <div class="updateUser">
              <b-modal id="modal-updateUser" title="Update Product" hide-footer>
                <b-form @submit.prevent="updateUser" @reset="onResetUser">
                    <b-form-group id="input-group-1" label="Email address:" label-for="input-1">
                      <b-form-input id="input-1" v-model="formSignupEdit.email" type="email" placeholder="Enter email to edit"
                        required></b-form-input>
                    </b-form-group>

                    <b-form-group id="input-group-2" label="Your Password:" label-for="input-2">
                      <b-form-input id="input-2" v-model="formSignupEdit.password" placeholder="Enter password to edit" required>
                      </b-form-input>
                    </b-form-group>

                    <b-form-group id="input-group-3" label="Your Name:" label-for="input-3">
                      <b-form-input id="input-3" v-model="formSignupEdit.name" placeholder="Enter name to edit" required>
                      </b-form-input>
                    </b-form-group>

                    <b-form-group id="input-group-4" label="Your Role:" label-for="input-">
                      <b-form-select id="input-4" v-model="formSignupEdit.role" :options="role" placeholder="Enter role to edit" required>
                      </b-form-select>
                    </b-form-group>



                    <b-button type="submit" variant="primary mr-2 mt-2">Submit</b-button>
                    <b-button type="reset" variant="danger mt-2">Reset</b-button>
                  </b-form>
              </b-modal>
            </div>

          </div>
        </div>
      </div>
    </div>



  </div>
</template>

<script scoped>
  import Navbar from '../components/Navbar.vue'
  import axios from 'axios';


  export default {
    components: {
      Navbar
    },
    name: 'settings',
    data() {
      return {
        perPageProduct: 5,
        currentPageProduct: 1,
        setproduct: [],
        fields: ['id', 'name', 'price', 'type', 'action'],

        formadd: {
          name: '',
          price: '',
          image: [],
          idcategory: null,
          type: null,
        },

        formeditproduct: {
          name: '',
          price: '',
          image: [],
          idcategory: null,
          type: null,
        },

        types: [{
          text: 'Select One',
          value: null
        }, 'Makanan', 'Minuman'],


        category: [{
          text: "Makanan",
          value: 1
        }, {
          text: "Minuman",
          value: 2
        }],



        perPageUser: 2,
        currentPageUser: 1,
        setUser: [],
        fieldsUser: ['id_user', 'name', 'email', 'role', 'action'],

        formSignup: {
          email: '',
          password: '',
          name: '',
          role: 'users',

        },

        formSignupEdit: {
          email: '',
          password: '',
          name: '',
          role: null,
        },

        role: [{
          text: 'Select One',
          value: null
        }, 'Admin', 'User'],





        perPageCategory: 2,
        currentPageCategory: 1,
        setCategory: [],
        fieldsCategory: ['id_category', 'type', 'Action'],

        formCategory: {
          type: '',

        },





      }
    },

    mounted() {
      this.getAllDataProduct()
      this.getAllDataUser()
      this.getAllDataCategory()
    },

    computed: {
      rowsproduct() {
        return this.setproduct.length
      },
      rowsUser() {
        return this.setUser.length
      },
      rowsCategory() {
        return this.setCategory.length
      }
    },

    methods: {


      onAddReset(evt) {
        evt.preventDefault()
        // Reset our form values
        this.formadd.name = ''
        this.formadd.price = ''
        this.formadd.image = ''
        this.formadd.idcategory = ''

        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },

       getAllDataProduct() {
        axios.get(process.env.VUE_APP_URL + 'product')
          .then(res => {
            this.setproduct = res.data.result
          })
          .catch(err => {
            console.log(err);
          })
      },

      onSubmitAdd() {
        let formProduct = new FormData();
        formProduct.append("name", this.formadd.name)
        formProduct.append("image", this.formadd.image)
        formProduct.append("price", this.formadd.price)
        formProduct.append("idcategory", this.formadd.idcategory)

        axios({
            method: 'post',
            url: process.env.VUE_APP_URL + 'product',
            headers: {
              "Content-type": "multipart/form-data",
              "authToken": this.$store.getters.getToken
            },
            data: formProduct
          })
          .then(res => {
            this.getAllDataProduct()
            console.log(res.data)
          })
          .catch(err => {
            console.log(err);
          })

      },

      onDeleteProduct(id) {
        console.log(id);
        axios({
            method: 'delete',
            url: process.env.VUE_APP_URL + `product/${id}`,
            headers: {
              "authToken": this.$store.getters.getToken
            }
          })
          .then(res => {
            this.getAllDataProduct()
            console.log(res.data)
          })
          .catch(err => {
            console.log(err);
          })

      },

      editProduct(value) {
        this.formeditproduct.id = value.id
        this.formeditproduct.name = value.name
        this.formeditproduct.price = value.price
        this.formeditproduct.image = value.image
        this.formeditproduct.type = value.type
      },

      onResetProduct(event) {
        event.preventDefault()
        this.formeditproduct.name = ''
        this.formeditproduct.price = ''
        this.formeditproduct.image = ''
        this.formeditproduct.type = ''
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },

      updateProduct() {
        let formData = new FormData();
        if (this.formeditproduct.image.length == undefined) {
          formData.append("image", this.formeditproduct.image);
        }
        if (
          this.formeditproduct.image.size > 3000000 &&
          !this.formeditproduct.image
        ) {
          alert("Too Large, max size allowed is 3 MB!");
        }
        if (this.formeditproduct.name != "") {
          formData.append("name", this.formeditproduct.name);
        }
        if (this.formeditproduct.price != "") {
          formData.append("price", this.formeditproduct.price);
        }
        if (this.formeditproduct.id_category != null) {
          formData.append("id_category", this.formeditproduct.id_category);
        }
        formData.append("id", this.formeditproduct.id);

        // authtoken: this.dataToken.token,
        axios({
            method: "PUT",
            url: process.env.VUE_APP_URL + "product",
            headers: {
              "Content-Type": "multipart/form-data"
            },
            data: formData,
          })
          .then((res) => {
            console.log("Masuk then");
            console.log(res);
            this.formEditProduct = [];
            alert(res.data.description);
            this.getAllProduct();
            this.resetData();
          })
          .catch((err) => {
            alert(err.message);
          });
      },







      getAllDataUser() {
        axios.get(process.env.VUE_APP_URL + 'users')
          .then(res => {
            this.setUser = res.data.result
          })
          .catch(err => {
            console.log(err);
          })
      },


      onSubmitSignup() {

        axios({
            method: "POST",
            url: process.env.VUE_APP_URL + "users",
            headers: {
              "Content-Type": "application/json",
              "authToken": this.$store.getters.getToken
            },
            data: this.formSignup,

          })
          .then((res) => {

            this.response = JSON.parse(JSON.stringify(res))
            this.$bvModal.hide("modal-addUser");
            this.getAllDataUser()
          })
          .catch(err => {
            console.log(err);
          })

      },

      editUser(value) {
        this.formSignupEdit.id = value.id
        this.formSignupEdit.email = value.email
        this.formSignupEdit.password = value.password
        this.formSignupEdit.name = value.name
        this.formSignupEdit.role = value.role
      },
      onResetUser(event) {
        event.preventDefault()
        this.formSignupEdit.name = ''
        this.formSignupEdit.price = ''
        this.formSignupEdit.image = ''
        this.formSignupEdit.type = ''
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      },


      onDeleteUser(id) {
        console.log(id);
        axios({
            method: 'delete',
            url: process.env.VUE_APP_URL + `users/${id}`,
            headers: {
              "authToken": this.$store.getters.getToken
            }
          })
          .then(res => {
            this.getAllDataUser()
            console.log(res.data)
          })
          .catch(err => {
            console.log(err);
          })

      },

      updateUser() {
        
        // authtoken: this.dataToken.token,
        axios({
            method: "PUT",
            url: process.env.VUE_APP_URL + "users",
            headers: {
              "authToken": this.$store.getters.getToken
            },
            data: this.formSignupEdit,
          })
          .then((res) => {
            console.log("Masuk then");
            console.log(res);
            this.formEditProduct = [];
            alert(res.data.description);
            this.getAllProduct();
            this.resetData();
          })
          .catch((err) => {
            alert(err.message);
          });
      }
      
      
      
      
      ,
      getAllDataCategory() {
        axios.get(process.env.VUE_APP_URL + 'category')
          .then(res => {
            this.setCategory = res.data.result
          })
          .catch(err => {
            console.log(err);
          })
      },










    }

  }
</script>


<style scoped>
  .header {
    z-index: 999;
    background-color: white;
    align-items: center;
    height: 100px;
    width: 95vw;
    padding-top: 20px;
  }

  .product {
    background-color: white;
    height: 50vh;
  }

  .user {
    background-color: white;
    height: 33vh;
  }

  .category {
    background-color: white;
    height: 33vh;
  }
</style>