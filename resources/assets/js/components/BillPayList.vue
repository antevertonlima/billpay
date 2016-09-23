<template>
    <div class="container">
        <div class="row">
            <a v-link="{name: 'bill-pay.create'}">
                <i class="material-icons">add_to_photos</i>
            </a>
            <table class="highlight striped">
            <thead>
              <tr>
                  <th data-field="id">Name</th>
                  <th data-field="name">Item Name</th>
                  <th data-field="price">Item Price</th>
              </tr>
            </thead>

            <tbody>
              <tr>
                <td>#</td>
                <td>Nome</td>
                <td>Vencimento</td>
                <td>Valor</td>
                <td>Ações</td>
              </tr>
              <tr v-for="(index, o) in bills">
                <td>{{ index + 1 }}</td>
                <td>{{ o.name }}</td>
                <td>{{ o.date_do }}</td>
                <td>{{ o.value }}</td>
                <td>
                    <a v-link="{name: 'bill-pay.update', params: {id: o.id}}">Editar</a> |
                    <a href="#" @click.prevent="destroy(o)">Excluir</a>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
    </div>
</template>

<style type="text/css">
    .container{
        min-height: 60%;
    }
</style>

<script>
    export default {
        data(){
            return {
                bills:[]
            };
        },
        methods: {
            destroy(o){
                this.$http.delete(`http://billpay.app/api/bill_pays/${o.id}`)
                          .then((response) => {
                            this.bills.$remove(o);
                            Materialize.toast('Conta removida com sucesso!', 4000);
                          })
            }
        },
        ready() {
            this.$http.get('http://billpay.app/api/bill_pays')
                      .then((response) => {
                        this.bills = response.data;
                      })
        }
    }
</script>
