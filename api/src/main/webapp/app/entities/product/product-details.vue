<template>
  <div class="row justify-content-center">
    <div class="col-8">
      <div v-if="product">
        <h2 class="jh-entity-heading" data-cy="productDetailsHeading"><span>Product</span> {{ product.id }}</h2>
        <dl class="row jh-entity-details">
          <dt>
            <span>Name</span>
          </dt>
          <dd>
            <span>{{ product.name }}</span>
          </dd>
          <dt>
            <span>Description</span>
          </dt>
          <dd>
            <span>{{ product.description }}</span>
          </dd>
          <dt>
            <span>Price</span>
          </dt>
          <dd>
            <span>{{ product.price }}</span>
          </dd>
          <dt>
            <span>Image</span>
          </dt>
          <dd>
            <span>{{ product.image }}</span>
          </dd>
          <dt>
            <span>Tva</span>
          </dt>
          <dd>
            <span>{{ product.tva }}</span>
          </dd>
          <dt>
            <span>Tva Take Away</span>
          </dt>
          <dd>
            <span>{{ product.tvaTakeAway }}</span>
          </dd>
          <dt>
            <span>Ingredient</span>
          </dt>
          <dd>
            <span v-for="(ingredient, i) in product.ingredients" :key="ingredient.id"
              >{{ i > 0 ? ', ' : '' }}
              <router-link :to="{ name: 'IngredientView', params: { ingredientId: ingredient.id } }">{{ ingredient.name }}</router-link>
            </span>
          </dd>
        </dl>
        <button type="submit" v-on:click.prevent="previousState()" class="btn btn-info" data-cy="entityDetailsBackButton">
          <font-awesome-icon icon="arrow-left"></font-awesome-icon>&nbsp;<span> Back</span>
        </button>
        <router-link v-if="product.id" :to="{ name: 'ProductEdit', params: { productId: product.id } }" custom v-slot="{ navigate }">
          <button @click="navigate" class="btn btn-primary">
            <font-awesome-icon icon="pencil-alt"></font-awesome-icon>&nbsp;<span> Edit</span>
          </button>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts" src="./product-details.component.ts"></script>
