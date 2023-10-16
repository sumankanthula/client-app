<template>
    <div>
        <b-card bg-variant="light">
            <b-form-group label-cols-lg="3" label="Product Search" label-size="lg" label-class="font-weight-bold pt-0"
                class="mb-0">
                <b-container class="bv-example-row">
                    <b-row>
                        <b-col>
                            <b-form-group label="Product#" label-for="inptProductId" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptProductId" v-model="searchData.productId"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Product Name" label-for="inptProductName" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptProductName" v-model="searchData.productName"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Supplier Id" label-for="inptSupplierId" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptSupplierId" v-model="searchData.supplierId"></b-form-input>
                            </b-form-group>
                        </b-col>
                    </b-row>
                    <b-row>
                        <b-col>
                            <b-form-group label="Category ID" label-for="inptCategoryID" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptCategoryID" v-model="searchData.categoryId"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Quantity/ Unit" label-for="inptQuantityPerUnit" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptQuantityPerUnit" v-model="searchData.quantityPerUnit"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Unit Price" label-for="inptUnitPrice" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptUnitPrice" v-model="searchData.unitPrice"></b-form-input>
                            </b-form-group>
                        </b-col>
                    </b-row>
                    <b-row>
                        <b-col>
                            <b-form-group label="Units InStock" label-for="inptUnitsInStock" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptUnitsInStock" v-model="searchData.unitsInStock"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Units OnOrder" label-for="inptUnitsOnOrder" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptUnitsOnOrder" v-model="searchData.unitsOnOrder"></b-form-input>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-form-group label="Reorder Level" label-for="inptReorderLevel" label-cols-sm="3"
                                label-align-sm="right">
                                <b-form-input id="inptReorderLevel" v-model="searchData.reorderLevel"></b-form-input>
                            </b-form-group>
                        </b-col>
                    </b-row>
                    <b-row>
                        <b-col>
                            <b-form-group label="Discontinued ?" v-slot="{ ariaDescribedby }">
                                <b-form-radio-group id="radio-group-2" v-model="searchData.discontinued"
                                    :aria-describedby="ariaDescribedby" name="radio-sub-component">
                                    <b-form-radio value="true">Yes</b-form-radio>
                                    <b-form-radio value="false">No</b-form-radio>
                                </b-form-radio-group>
                            </b-form-group>
                        </b-col>
                        <b-col>
                            <b-button type="submit" @click="searchProduct" variant="outline-primary">Search</b-button>
                        </b-col>
                        <b-col></b-col>
                    </b-row>

                    <b-row>
                        <div class="overflow-auto">
                            <b-pagination v-model="searchData.currentPage" :total-rows="searchData.result.length"
                                :per-page="searchData.perPage" aria-controls="my-table"></b-pagination>

                            <p class="mt-3">Current Page: {{ searchData.currentPage }}</p>

                            <b-table id="my-table" :items="searchData.result" :per-page="searchData.perPage"
                                :current-page="searchData.currentPage" small></b-table>
                        </div>
                    </b-row>

                </b-container>
            </b-form-group>
        </b-card>
    </div>
</template>
  
<script>
import axios from 'axios';

export default {

    data() {
        return {
            searchData: {
                productId: null,
                productName: '',
                supplierId: null,
                categoryId: null,
                quantityPerUnit: '',
                unitPrice: null,
                unitsInStock: null,
                unitsOnOrder: null,
                reorderLevel: null,
                discontinued: null,

                perPage: 10,
                currentPage: 1,

                result: []
            }
        };
    },
    methods: {

        searchProduct() {
            console.log('search btn clicked...')
            console.log(this.searchData.discontinued);
            this.searchData.result = [];
            axios.post('http://localhost:62924/api/Products/Search', this.searchData).then(res => {
                console.log(res);
                this.searchData.result = res.data;
            })
        },


    },
};
</script>
  