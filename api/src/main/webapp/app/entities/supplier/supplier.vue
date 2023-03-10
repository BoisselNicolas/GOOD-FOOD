<template>
  <div>
    <h2 id="page-heading" data-cy="SupplierHeading">
      <span id="supplier-heading">Suppliers</span>
      <div class="d-flex justify-content-end">
        <button class="btn btn-info mr-2" v-on:click="handleSyncList" :disabled="isFetching">
          <font-awesome-icon icon="sync" :spin="isFetching"></font-awesome-icon> <span>Refresh List</span>
        </button>
        <router-link :to="{ name: 'SupplierCreate' }" custom v-slot="{ navigate }">
          <button
            @click="navigate"
            id="jh-create-entity"
            data-cy="entityCreateButton"
            class="btn btn-primary jh-create-entity create-supplier"
          >
            <font-awesome-icon icon="plus"></font-awesome-icon>
            <span> Create a new Supplier </span>
          </button>
        </router-link>
      </div>
    </h2>
    <br />
    <div class="alert alert-warning" v-if="!isFetching && suppliers && suppliers.length === 0">
      <span>No suppliers found</span>
    </div>
    <div class="table-responsive" v-if="suppliers && suppliers.length > 0">
      <table class="table table-striped" aria-describedby="suppliers">
        <thead>
          <tr>
            <th scope="row"><span>ID</span></th>
            <th scope="row"><span>Name</span></th>
            <th scope="row"><span>Description</span></th>
            <th scope="row"><span>Number</span></th>
            <th scope="row"><span>Address</span></th>
            <th scope="row"><span>Ingredient</span></th>
            <th scope="row"></th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="supplier in suppliers" :key="supplier.id" data-cy="entityTable">
            <td>
              <router-link :to="{ name: 'SupplierView', params: { supplierId: supplier.id } }">{{ supplier.id }}</router-link>
            </td>
            <td>{{ supplier.name }}</td>
            <td>{{ supplier.description }}</td>
            <td>{{ supplier.number }}</td>
            <td>{{ supplier.address }}</td>
            <td>
              <div v-if="supplier.ingredient">
                <router-link :to="{ name: 'IngredientView', params: { ingredientId: supplier.ingredient.id } }">{{
                  supplier.ingredient.name
                }}</router-link>
              </div>
            </td>
            <td class="text-right">
              <div class="btn-group">
                <router-link :to="{ name: 'SupplierView', params: { supplierId: supplier.id } }" custom v-slot="{ navigate }">
                  <button @click="navigate" class="btn btn-info btn-sm details" data-cy="entityDetailsButton">
                    <font-awesome-icon icon="eye"></font-awesome-icon>
                    <span class="d-none d-md-inline">View</span>
                  </button>
                </router-link>
                <router-link :to="{ name: 'SupplierEdit', params: { supplierId: supplier.id } }" custom v-slot="{ navigate }">
                  <button @click="navigate" class="btn btn-primary btn-sm edit" data-cy="entityEditButton">
                    <font-awesome-icon icon="pencil-alt"></font-awesome-icon>
                    <span class="d-none d-md-inline">Edit</span>
                  </button>
                </router-link>
                <b-button
                  v-on:click="prepareRemove(supplier)"
                  variant="danger"
                  class="btn btn-sm"
                  data-cy="entityDeleteButton"
                  v-b-modal.removeEntity
                >
                  <font-awesome-icon icon="times"></font-awesome-icon>
                  <span class="d-none d-md-inline">Delete</span>
                </b-button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <b-modal ref="removeEntity" id="removeEntity">
      <span slot="modal-title"
        ><span id="goodfoodApp.supplier.delete.question" data-cy="supplierDeleteDialogHeading">Confirm delete operation</span></span
      >
      <div class="modal-body">
        <p id="jhi-delete-supplier-heading">Are you sure you want to delete this Supplier?</p>
      </div>
      <div slot="modal-footer">
        <button type="button" class="btn btn-secondary" v-on:click="closeDialog()">Cancel</button>
        <button
          type="button"
          class="btn btn-primary"
          id="jhi-confirm-delete-supplier"
          data-cy="entityConfirmDeleteButton"
          v-on:click="removeSupplier()"
        >
          Delete
        </button>
      </div>
    </b-modal>
  </div>
</template>

<script lang="ts" src="./supplier.component.ts"></script>
