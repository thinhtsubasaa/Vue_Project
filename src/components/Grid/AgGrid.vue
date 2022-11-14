<template>
  <div class="content">
    <div><button style="margin-left:50%" class="btn btn-success" @click="openModal">Add</button></div>
    <div>
      <ag-grid-vue style="width: 100%; height: 250px;" class="ag-theme-alpine" :columnDefs="columnDefs"
        :rowData="rowData" />

      <b-modal id="modal-1" title="AgGird" v-model="isShowModal" @hidden="callOnHide" @ok="handleOk">
        <template #modal-header>
          <!-- Emulate built in modal header close button action -->
          <h5>{{ modal.title }}</h5>
        </template>
        <template #default>
          <p>{{ modal.message }}</p>
          <div v-if="modal.type === 'ADD'">
            <div>
              <span>Make </span>
              <input type="text" v-model="make">
            </div>
            <div>
              <span>Model</span>
              <input type="text" v-model="model">
            </div>
            <div>
              <span>Price: </span>
              <input type="number" v-model="price">
            </div>
          </div>
          <div v-else-if="modal.type === 'DELETE'">
            <p>Product detail: {{ deleteObject.make }} {{ deleteObject.model }} {{ deleteObject.price }}</p>
          </div>
          <div v-if="modal.type === 'EDIT'">
            <div>
              <span>Make </span>
              <input type="text" v-model="editObject.make">
            </div>
            <div>
              <span>Model</span>
              <input type="text" v-model="editObject.model">
            </div>
            <div>
              <span>Price: </span>
              <input type="number" v-model="editObject.price">
            </div>
          </div>


        </template>

      </b-modal>
    </div>

  </div>
</template>

<script>
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import CellButton from "../common/cellRender/CellButton.vue";
import { AgGridVue } from "ag-grid-vue";
import _ from 'lodash';
import CellEdit from '../common/cellRender/CellEdit.vue'
export default {
  name: 'AgGird',
  components: {
    AgGridVue,
    // eslint-disable-next-line
    CellButton,
    // eslint-disable-next-line
    CellEdit
  },
  data() {
    return {
      columnDefs: null,
      rowData: null,
      make: null,
      model: null,
      price: null,
      showAgGird: false,
      modal: {
        title: 'modal title',
        message: 'message',
        type: 'ADD'
      },
      isShowModal: false,
      deleteObject: {},
      editObject: {}
    }
  },
  props: {
  },

  watch: {
    isShowAgGird(value) {
      console.log("login: ", value)
      this.showAgGird = value

    },
  },

  beforeMount() {
    this.columnDefs = [
      { field: "make" },
      { field: "model" },
      { field: "price" },
      {
        headerName: 'Delete',
        cellRenderer: 'CellButton',
        cellRendererParams: {
          text: 'Delete',
          onBtnClick: this.deleteCell
        }
      },
      {
        headerName: 'Edit',
        cellRenderer: 'CellEdit',
        cellRendererParams: {
          text: 'Edit',
          onBtnClick: this.editCell
        }
      },
    ];
    this.rowData = [
      { make: "Toyota", model: "Celica", price: 35000 },
      { make: "Ford", model: "Mondeo", price: 32000 },
      { make: "Porsche", model: "Boxster", price: 72000 },
    ];
  },
  methods: {
    deleteCell(rowData) {
      console.log('deleteCell: ', rowData)
      this.deleteObject = rowData
      this.modal = {
        title: 'Delete',
        type: 'DELETE',
        message: 'This action will delete the product below'
      }
      this.isShowModal = true
    },
    editCell(rowData) {
      console.log('editCell: ', rowData)
      this.editObject = rowData
      this.modal = {
        title: 'Edit',
        type: 'EDIT',
        message: 'This action will edit the product below'
      }
      this.isShowModal = true
    },
    add() {

      this.rowData.push({
        make: this.make,
        model: this.model,
        price: this.price
      })
    },
    handleOk() {
      if (this.modal.type === 'ADD') {
        console.log('Ok');
        this.add();
      }
      else if (this.modal.type === 'DELETE') {
        console.log('delete')
        this.removeProduct()
      } else if (this.modal.type === 'EDIT') {
        console.log('edit')
        this.editProduct()
      }
    },
    removeProduct() {
      const { make, price, model } = this.deleteObject
      const products = _.clone(this.rowData)
      _.remove(products, (prod) => { return prod.make === make && prod.model === model && prod.price === price })
      this.rowData = products
    },
    editProduct() {
      const { make, price, model } = this.editObject
      const product = _.clone(this.rowData)
      _.map(product, (prod) => { return prod.make === make && prod.price === price && prod.model === model })
      this.rowData = product
    },

    openModal() {
      this.modal = {
        title: 'Add new product',
        message: 'Input product detail',
        type: 'ADD'
      }
      console.log('showAg')
      this.isShowModal = true
    },
    callOnHide() {
      this.isShowModal = false
      this.modal = {}
    }

  }

}
</script>

<style scoped>
@import "~ag-grid-community/styles/ag-grid.css";
@import "~ag-grid-community/styles/ag-theme-alpine.css";
</style>