<template>

    <div>
        <div class="detail-title">
        SalesItem
        </div>
        <v-col>
            <div class="label-title">이름</div>
            <String label="이름" v-model="value.name" :editMode="editMode"/>
            <div class="label-title">가격</div>
            <Number label="가격" v-model="value.price" :editMode="editMode"/>
            <div class="label-title">수량</div>
            <Number label="수량" v-model="value.qty" :editMode="editMode"/>
            <ProductId offline label="ProductId" v-model="value.productId" :editMode="editMode" @change="change"/>
        </v-col>

        <v-card-actions v-if="inList">
            <slot name="actions"></slot>
        </v-card-actions>
    </div>
</template>

<script>
import BaseEntity from './base-ui/BaseEntity'

export default {
    name: 'SalesItem',
    mixins:[BaseEntity],
    components:{
    },
    data: () => ({
        path: 'SalesItems',
    }),
    watch: {
        value(val){
            this.value = val;
            this.change();
        },
    },
    async created(){
        if (this.value && this.value.id !== undefined) {
            this.value = await this.repository.findById(this.value.id)
        }
    },
    methods: {
        pick(val){
            this.value = val;
            this.change();
        },
    }
}
</script>

