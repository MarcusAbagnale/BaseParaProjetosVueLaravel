<template>
  <v-container>
    <v-btn @click="openCreateDialog">Criar Produto</v-btn>
    
    <v-data-table :items="products" :headers="headers">
      <template v-slot:item.actions="{ item }">
        <v-btn @click="openEditDialog(item)">Editar</v-btn>
        <v-btn @click="deleteProduct(item.id)" color="red">Deletar</v-btn>
      </template>
    </v-data-table>

    <!-- Dialog para Criar Produto -->
    <v-dialog v-model="createDialog" max-width="600px">
      <v-card>
        <v-card-title>
          <span class="headline">Criar Produto</span>
        </v-card-title>
        <v-card-text>
          <v-text-field v-model="newProduct.name" label="Nome" required></v-text-field>
          <v-text-field v-model="newProduct.slug" label="Slug" required></v-text-field>
          <v-textarea v-model="newProduct.description" label="Descrição"></v-textarea>
          <v-text-field v-model="newProduct.price" label="Preço" type="number" step="0.01" required></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="createDialog = false">Cancelar</v-btn>
          <v-btn color="primary" @click="createProduct">Criar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>

    <!-- Dialog para Editar Produto -->
    <v-dialog v-model="editDialog" max-width="600px">
      <v-card>
        <v-card-title>
          <span class="headline">Editar Produto</span>
        </v-card-title>
        <v-card-text>
          <v-text-field v-model="editedProduct.name" label="Nome" required></v-text-field>
          <v-text-field v-model="editedProduct.slug" label="Slug" required></v-text-field>
          <v-textarea v-model="editedProduct.description" label="Descrição"></v-textarea>
          <v-text-field v-model="editedProduct.price" label="Preço" type="number" step="0.01" required></v-text-field>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn text @click="editDialog = false">Cancelar</v-btn>
          <v-btn color="primary" @click="updateProduct">Salvar</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      products: [],
      headers: [
        { text: 'Nome', value: 'name' },
        { text: 'Slug', value: 'slug' },
        { text: 'Descrição', value: 'description' },
        { text: 'Preço', value: 'price' },
        { text: 'Ações', value: 'actions', sortable: false },
      ],
      createDialog: false,
      editDialog: false,
      newProduct: {
        name: '',
        slug: '',
        description: '',
        price: '',
      },
      editedProduct: {},
    };
  },
  methods: {
    async fetchProducts() {
      const token = localStorage.getItem('authToken');
      try {
        const response = await axios.get(`${import.meta.env.VITE_API_BASE_URL}/api/products`, {
          headers: { 'Authorization': `Bearer ${token}` },
        });
        this.products = response.data;
      } catch (error) {
        console.error('Erro ao buscar produtos:', error);
      }
    },
    async createProduct() {
      const token = localStorage.getItem('authToken');
      try {
        await axios.post(`${import.meta.env.VITE_API_BASE_URL}/api/products`, this.newProduct, {
          headers: { 'Authorization': `Bearer ${token}` },
        });
        this.fetchProducts();
        this.createDialog = false;
        this.newProduct = { name: '', slug: '', description: '', price: '' };
      } catch (error) {
        console.error('Erro ao criar produto:', error);
      }
    },
    async updateProduct() {
      const token = localStorage.getItem('authToken');
      try {
        await axios.put(`${import.meta.env.VITE_API_BASE_URL}/api/products/${this.editedProduct.id}`, this.editedProduct, {
          headers: { 'Authorization': `Bearer ${token}` },
        });
        this.fetchProducts();
        this.editDialog = false;
      } catch (error) {
        console.error('Erro ao editar produto:', error);
      }
    },
    async deleteProduct(productId) {
      const token = localStorage.getItem('authToken');
      try {
        await axios.delete(`${import.meta.env.VITE_API_BASE_URL}/api/products/${productId}`, {
          headers: { 'Authorization': `Bearer ${token}` },
        });
        this.fetchProducts();
      } catch (error) {
        console.error('Erro ao deletar produto:', error);
      }
    },
    openCreateDialog() {
      this.createDialog = true;
    },
    openEditDialog(product) {
      this.editedProduct = { ...product };
      this.editDialog = true;
    },
  },
  mounted() {
    this.fetchProducts();
  },
};
</script>
