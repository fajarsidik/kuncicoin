<template>
    <div>
        <div class="flex justify-center align-center">
            <table class="table">
                <thead>
                     <th>
                        No
                    </th>
                    <th>
                        Master
                    </th>
                    <th>
                        Slave
                    </th>                   
                </thead>

                <tbody>
                    <tr v-for="(item, key) in list" :key='key'>
                        <td>{{key+1}}</td>
                        <td>{{item.master}}</td>
                        <td>{{item.slave}}</td>                       
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>

<script>
export default {
  name: 'List',  
  props: {
    data: Object
  },
   data(){
    return{
      list : this.data
    }
  },
  methods: {
      add(){
        this.list.push({ master: 'hgfs', slave: 'bbfsbbbgf' })
      },
      remove(index){
        this.list.splice(index, 1);
      }
  }
}
</script>

<style lang="scss" scoped>

.table{
    width: 50%;
    border-collapse: collapse;
    margin: 25px 0;
    font-size: 0.9em;
    font-family: sans-serif;
    min-width: 400px;
    box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
    border-radius: 4px;

    thead{
        th{
            background-color: #6f3792;
            color: #ffffff;
            text-align: left;
            
            &:first-child{
                border-radius: 4px 0 0 0;
            }
            &:last-child{
                border-radius: 0 4px 0 0;
            }
        }
    }

    th,
    td{
        padding: 12px 15px;
    }

    tbody{
        tr{
            border-bottom: 1px solid #dddddd;

            &:nth-of-type(even){
                background-color: #f3f3f3;
            }

            &:last-of-type{
                border-bottom: 2px solid #6f3792;
            }
        }
    }
}
</style>