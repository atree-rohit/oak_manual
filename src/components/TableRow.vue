<style scoped>
td{
    padding: 0 1rem;
}
.id-row{
    padding: 0 1rem;
}
</style>

<template>
  <tr>
    <td class="id-row">{{ convertToRoman(data_id) }}</td>
    <td class="data-row">{{ data_data }}</td>
  </tr>
</template>



<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'TableRow',
  props: ["data"],
  computed: {
    data_split() {
      return this.data.split(". ")
    },
    data_id(){
        return this.data_split[0]
    },
    data_data(){
        return this.data_split[1]
    }
  },
  methods:{
    convertToRoman(num) {
        const romanNumerals = [
            { value: 1000, numeral: 'm' },
            { value: 900, numeral: 'cm' },
            { value: 500, numeral: 'd' },
            { value: 400, numeral: 'cd' },
            { value: 100, numeral: 'c' },
            { value: 90, numeral: 'xc' },
            { value: 50, numeral: 'l' },
            { value: 40, numeral: 'xl' },
            { value: 10, numeral: 'x' },
            { value: 9, numeral: 'ix' },
            { value: 5, numeral: 'v' },
            { value: 4, numeral: 'iv' },
            { value: 1, numeral: 'i' }
        ];

        let result = '';

        for (let i = 0; i < romanNumerals.length; i++) {
            while (num >= romanNumerals[i].value) {
            result += romanNumerals[i].numeral;
            num -= romanNumerals[i].value;
            }
        }

        return result;
    }
  }
})
</script>