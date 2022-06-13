<template>
    <div class="text-center  mt-5 w-600 h-20 pt-7 mb-5 mx-5 ">
        <select @change="onChange()" v-model="selected" class="text-sm form-select mt-1 block w-full border p-3 rounded" :required = "true">
            <option value="0">Choose Country</option>
            <option v-for="country in countries"  :value="country.ID" :key="country.ID">
                {{country.Country}}
            </option>
        </select>
        
    </div>
    
</template>

<script>
    export default {
        name: "CountrySelect",
        props: ["countries"],
        data(){
            return {
            selected: 0,
        }
        },
         methods: {
            onChange(){
            const country = this.countries.find((item)=> item.ID === this.selected)
            console.log(country)
            this.$emit('get-country',country)
            }
         }
    }
</script>