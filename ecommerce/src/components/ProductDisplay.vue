<template>
    <div class="background">
        <div id="bg-pattern"
            :style="[
                products.category === `men's clothing` ? { backgroundColor: '#D6E6FF' } : {},
                products.category === `women's clothing` ? { backgroundColor: '#FDE2FF' } : {},
                products.category === `jewelery` || products.category === `electronics` ? { backgroundColor: '#D8D7D7'} : {}
            ]"></div>
        <div class="products-invalid"
            :style="[products.category === `men's clothing` || products.category === `women's clothing` ? { display: 'none'} : {}]"
        >
            <div class="pi-center">
                <h3>This product is unavailable to show</h3>
                <button @click="nextPage">Next Product</button>
            </div>
        </div>
        <div class="products"
            :style="[products.category === `men's clothing` || products.category === `women's clothing` ? {} : { display: 'none' }]"
        >
            <!-- <div v-if="loading" class="loader"></div> -->
            <div class="p-left">
                <img :src='products.image' alt="product image">
            </div>
            <div class="p-right">
                <div class="pr-1">
                    <p2 :style="[products.category === `men's clothing` ? { color: '#002772' } : { color: '#720060' }]"
                    >{{ products.title }}</p2>
                    <div class="category">
                        <p>{{ products.category }}</p>
                        <div class="rating">
                            <p>{{rating.rate}}/5</p>
                            <span >
                                <div id="circle1"
                                    :style="[products.category === `men's clothing` ? { background: '#002772', border: '1px solid #002772' } : { background: '#720060', border: '1px solid #720060' }]"></div>
                                <div id="circle1"
                                    :style="[products.category === `men's clothing` ? { background: '#002772', border: '1px solid #002772' } : { background: '#720060', border: '1px solid #720060' }]"></div>
                                <div id="circle1"
                                    :style="[products.category === `men's clothing` ? { background: '#002772', border: '1px solid #002772' } : { background: '#720060', border: '1px solid #720060' }]"></div>
                                <div id="circle2"
                                    :style="[products.category === `men's clothing` ? { border: '1px solid #002772' } : { border: '1px solid #720060' }]"></div>
                                <div id="circle2"
                                    :style="[products.category === `men's clothing` ? { border: '1px solid #002772' } : { border: '1px solid #720060' }]"></div>
                            </span>
                        </div>
                    </div>
                </div>
                <div class="pr-2">
                    <hr/>
                    <p>{{ products.description }}</p>
                </div>
                <div class="pr-3">
                    <hr/>
                    <p :style="[products.category === `men's clothing` ? { color: '#002772' } : { color: '#720060' }]">
                        ${{ products.price }}</p>
                    <span>
                        <button id="bl" :style="[products.category === `men's clothing` ? { backgroundColor: '#002772', border: '1px solid #002772' } : { backgroundColor: '#720060', border: '1px solid #720060' }]"
                            >Buy now</button>
                        <button @click="nextPage" :style="[products.category === `men's clothing` ? { color: '#002772', border: '3px solid #002772' } : { color: '#720060', border: '3px solid #720060' }]"
                            >Next Product</button>
                    </span>
                    
                </div>

            </div>
        </div>
    </div>

</template>

<script>
export default {
    name: 'ProductDisplay',
    data() {
        return {
            loading: false,
            products: [],
            rating: [],
            paramIndex: 1
        }
    },
    mounted() {
        this.fetchProduct()
    }, methods: {
        fetchProduct() {
            this.loading = true
            fetch(`https://fakestoreapi.com/products/${this.paramIndex}`)
                .then(res => res.json())
                .then(data => {
                    this.loading = false
                    this.products = data
                    this.rating = data.rating
                })
                .catch(err => console.log(err.message))
        },
        nextPage() {
            this.paramIndex++
            if (this.paramIndex > 20) {
                this.paramIndex = 1
                this.fetchProduct()
            }
            this.fetchProduct()
        }
    }
}
</script>