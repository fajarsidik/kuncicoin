<template>
    <div>
        <div class="flex justify-center align-center add-btn">
             <button type="button" class="add" @click="addProduct()">
                    + Add Product
                </button>
        </div>
        <div class="flex justify-center align-center">
            
            <table class="table">
                <thead>
                     <th>
                        No
                    </th>
                    <th>
                        Product
                    </th>
                    <th>
                        Price
                    </th>
                    <th>
                        Quantity
                    </th>
                    <th>
                        Action
                    </th>
                </thead>

                <tbody>
                    <tr v-for="(item, key) in list" :key='key'>
                        <td>{{key+1}}</td>
                        <td>{{item.productName}}</td>
                        <td>{{item.price}}</td>
                        <td>{{item.quantity}}</td>                        
                        <td>
                            <div class="flex justify-start action">                               
                                <a href="#" title="Edit" @click="update(item.id)"><img src="@/assets/img/edit.png" alt="" /></a>                               
                                <a href="#" title="Delete" @click="confirmDelete(key)"><img src="@/assets/img/delete.png" alt="" /></a>
                            </div>
                        </td>
                    </tr>
                </tbody>
            </table>

            <div class="popup" :class="isShowDelete ? 'show-delete' : ''">
                <div class="modal">
                    <p>Are you sure want to delete ?</p>
                    <div class="flex justify-center">
                        <button type="button" class="cancel" @click="isShowSidebar = !isShowSidebar">
                            Cancel
                        </button>
                        <button type="button" class="add" @click="remove(keyProduct)">
                            Yes, Sure
                        </button>
                    </div>
                </div>
            </div>

            <div class="container" :class="isShowSidebar ? 'show-sidebar' : ''">
                <div class="form-input">
                    <h2>Add Product</h2>
                        <div v-if="errors.length" class="error">
                            <p>Please correct the following error(s):</p>
                            <ul>
                                <li v-for="(error,key) in errors" :key="key">{{ error }}</li>
                            </ul>
                        </div>
                    <div class="form-group">
                        <label for="product">Product Name</label>
                        <input type="text" placeholder="Insert product name here..." v-model="productName">
                    </div>

                    <div class="form-group">
                        <label for="product">Price</label>
                        <input type="text" placeholder="Insert price here..." v-model="price" @keypress="validateNumber" @blur="validateNumber">
                    </div>
                    <div class="form-group">
                        <label for="product">Quantity</label>
                        <input type="text" placeholder="Insert quantity here..." v-model="quantity" @keypress="validateNumber">
                    </div>

                    <div class="flex justify-end">
                        <button type="button" class="cancel" @click="isShowSidebar = !isShowSidebar">
                            Cancel
                        </button>
                        <button type="button" class="add" @click="isUpdate ? updateProduct() : checkProduct()">
                            {{isUpdate ? 'Update Product ' : '+ Add Product'}}
                        </button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'ListProduct',  
  props: {
    data: Object
  },
   data(){
    return{
      list : this.data,
      id: 1,
      productName: '',
      price: '',
      quantity: '',
      errors: [],
      isShowSidebar: false,
      isShowDelete: false,
      isUpdate: false,
      keyProduct:''
    }
  },
  methods: {
      add(){
        this.list.push({ id: this.id + 1, productName: this.productName, price: this.price, quantity: this.quantity })
      },
      addProduct(){
          this.productName = '',
          this.price = '',
          this.quantity = '',
          this.keyProduct = '',
          this.isShowSidebar = !this.isShowSidebar
      },
      update(id){
       let objIndex = this.list.findIndex((obj => obj.id == id))

       this.productName = this.list[objIndex].productName
       this.price = this.list[objIndex].price
       this.quantity = this.list[objIndex].quantity
       this.keyProduct = id
       this.isUpdate = true
       this.isShowSidebar = !this.isShowSidebar
      },
      remove(index){
        this.list.splice(index, 1);
        this.isShowDelete = !this.isShowDelete
      },
      confirmDelete(index){
          this.isShowDelete = !this.isShowDelete
          this.keyProduct = index
      },
      checkProduct(){
            
            this.errors = [];
            if (!this.productName || this.price || this.quantity) {
                this.errors.push('All field are required.');
            } 
                        
            if (this.productName && this.price && this.quantity) {
                this.errors = [];
                this.add()
                return true;
            }
           
      },

      updateProduct(){
            
            this.errors = [];
            if (!this.productName || this.price || this.quantity) {
                this.errors.push('All field are required.');
            } 
                        
            if (this.productName && this.price && this.quantity) {
                this.errors = [];
                let objIndex = this.list.findIndex((obj => obj.id == this.keyProduct))
                this.list[objIndex].productName = this.productName
                this.list[objIndex].price = this.price
                this.list[objIndex].quantity = this.quantity
                this.isShowSidebar = !this.isShowSidebar
                return true;
            }
           
      },
      validateNumber: evt => {
        evt = (evt) ? evt : window.event;
            var charCode = (evt.which) ? evt.which : evt.keyCode;
            if ((charCode > 31 && (charCode < 48 || charCode > 57)) && charCode !== 46) {
                evt.preventDefault()
            } else {
                return true;
            }
      }
  }
}
</script>

<style lang="scss" scoped>
.add-btn{
    margin: 20px 0;
}
.table{
    width: 50%;
    border-collapse: collapse;
    margin: 25px 0;
    font-size: 0.9em;
    font-family: sans-serif;
    min-width: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    border-radius: 4px;

    thead{
        th{
            background-color: #6f3792;
            color: #ffffff;
            text-align: left;
            
            &:first-child{
                border-radius: 4px 0 0 0;
            }
            &:last-child{
                border-radius: 0 4px 0 0;
            }
        }
    }

    th,
    td{
        padding: 12px 15px;
    }

    tbody{
        tr{
            border-bottom: 1px solid #dddddd;

            &:nth-of-type(even){
                background-color: #f3f3f3;
            }

            &:last-of-type{
                border-bottom: 2px solid #6f3792;
            }

            td{
                .action{
                    a{
                        margin-right: 10px;
                    }                    
                }
            }
        }
    }
}

/** Form Input */
.container{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
     &::after{
        content:'';
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0,0,0,0.5);
    }
    opacity: 0;
    visibility: hidden;
    transition: .3s;


    &.show-sidebar{
        opacity: 1;
        visibility: visible;
    }
}
.form-input{
    background-color: #fff !important;
    box-shadow: 0 1px 5px rgba(0,0,0,0.1);
    padding: 30px;
    border-radius: 6px 0 0 6px;
    position: absolute;
    right: 0;
    top: 0;
    height: 100vh;
    width: 400px;
    z-index: 1;
   
    h2{
        color: #000;
        font-size: 18px;
        padding-bottom: 10px;
        border-bottom: 1px solid #eee;
    }
}

.form-group{
    display: flex;
    flex-direction: column;
    margin-bottom: 20px;
    label{
        font-size: 14px;
        margin-bottom: 10px;
    }
    input[type="text"]{
        border-radius: 4px;
        border: 1px solid #eee;
        box-shadow: none;
        padding: 8px 15px;
        font-size: 12px;
    }   
}

 button{
        font-size: 12px;
        font-weight: 600;
        box-shadow: none;
        border: none;
        padding: 10px 20px;
        border-radius: 6px;
        margin-left: 20px;
        cursor: pointer;

        &.add{
            background: linear-gradient(90.58deg,#532bdc 0.3%,#7656e3);
            color: #fff;
        }
        
    }

    .error{
        
        margin-bottom: 20px;
        border-bottom: 1px solid #eee;
        p{
            font-size: 12px;
            font-weight: 600;
            
        }
        ul{
            margin-left: 0;
            padding-left: 0;
            li{
                list-style:none ;
                font-size: 12px;
                font-weight: bold;
                color: #ff4e4e;
            }
        }
    }

.popup{
    position: fixed;
    background-color: rgba(0,0,0,0.5);
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    opacity: 0;
    visibility: hidden;
    transition: .3s;

    &.show-delete{
        opacity: 1;
        visibility: visible;        
    }
    .modal{
        width: 400px;
        background: #fff;
        box-shadow: 0 1px 5px rgba(0,0,0,0.1);
        padding: 30px 50px;
        border-radius: 6px;
        display: flex;
        flex-direction: column;
        justify-content: center;
        p{
            text-align: center;
        }
    }
}
</style>