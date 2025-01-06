<template>
    <div class="fixed top-0 left-0 h-full w-full bg-black z-10 opacity-70"></div>
    <div class="flex flex-col justify-between fixed h-full z-20 top-0 h-full right-0 w-96 bg-white px-10 py-7">
 
        <DrawerHead :closeDrawer="closeDrawer"/>

        <div v-if="!totalPrice || orderId" class="flex h-full items-center">
            <InfoBlock 
                v-if="!totalPrice && !orderId"
                title="Shopping Cart is empty" 
                description="Add at least one pair of sneakers to complete your order." 
                image-url="/package-icon.png" />

            <InfoBlock
                v-if="orderId"
                title="Order is processed!!"
                :description="`Your order #${orderId} will soon be transferred to courier delivery`"
                image-url="/order-success-icon.png" />
        </div>


        <div v-else class="flex flex-col flex-1 justify-between">
            <div class="flex flex-col gap-5">
                <CartItemList :cart="carts" :deleteToCart="deleteToCart"/>
            </div>

            <div>
                <div class="flex flex-col gap-5">
                    <div class="flex items-end gap-2">
                        <span>Total:</span>
                        <div class="flex-1 border-b border-dashed" />
                        <span class="font-bold">{{totalPrice}} dram.</span>
                    </div>

                    <div class="flex items-end gap-2">
                        <span>Tax 5%:</span>
                        <div class="flex-1 border-b border-dashed" />
                        <span class="font-bold">{{ taxPersent }} dram.</span>
                    </div>
                    <div class="flex items-end gap-2">
                        <span>Sum:</span>
                        <div class="flex-1 border-b border-dashed" />
                        <span class="font-bold">{{ Math.round(totalPrice + taxPersent)}} dram.</span>
                    </div>
                </div>
                
                <button :disabled="orderButtonDdisabled" @click="createOrder" 
                    class="flex justify-center items-center gap-3 w-full py-3 mt-10 bg-lime-500 text-white rounded-xl transition active:bg-lime-700 hover:bg-lime-600 disabled:bg-slate-300  cursor-pointer"
                >
                    Order checkout
                    <img src="/arrow-next.svg" alt="Arrow" />
                </button>

            </div>
        </div>
    </div>

</template>

<script>
import axios from 'axios';
import CartItemList from './CartItemList.vue';
import DrawerHead from './DrawerHead.vue';
import InfoBlock from './InfoBlock.vue'

export default {
    // inject: ['products'],
    components: {
        CartItemList, DrawerHead, InfoBlock
    },
    data() {
        return {
            isCreatingOrder: false,
            orderId: null,
            carts: this.cart,
        }
    },
    props: {
        closeDrawer: {
            type: Function,
            required: true
        },
        cart: {
            type: Array,
            required: true
        },
        totalPrice: {
            type: Number,
            required: true
        },
        taxPersent: {
            type: Number,
            required: true
        },
        deleteToCart: {
            type: Function,
            required: true
        }
    },
    computed: {
        orderButtonDdisabled(){
            return (this.isCreatingOrder || this.carts.length === 0 )
        },
    },
    methods: {
        createOrder() {
            try {
                this.isCreatingOrder = true
                console.log(this.carts)
                axios.post(`https://67e54f4bc6572184.mokky.dev/orders`, 
                        {items: this.carts, totalPrice: this.totalPrice})
                .then((response) => { 

                    console.log(response.data)
                    this.orderId = response.data.id
                    //return response.data 
                    
                })

                this.carts = []
                location.reload();
                // console.log(this.carts)
                // this.closeDrawer()
            } catch(err) {
                console.log(err)
            }
            finally{
                this.isCreatingOrder = false
            }
        },
    },
    watch: {
        carts: {
            handler(newValue, oldValue){
                console.log(oldValue)
                console.log('kkkk8')
                console.log(newValue)
            },
            deep: true,
            

        // this.products.map((prod) => {
        //     if(prod.isAdded) {
        //     prod.isAdded = false
        //     }
        // })
        
        }
    }
}
</script>