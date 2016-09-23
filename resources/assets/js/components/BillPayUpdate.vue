<template>
    <div class="container">
        <div class="row">
            <form>
                <legend>Edição de conta a pagar.</legend>

                <div class="input-field">
                    <input type="text" v-model="bill.name" id="name" placeholder="Nome. Ex.: Cartão">
                </div>

                <div class="input-field">
                    <input type="text" v-model="bill.date_do" id="date_do" placeholder="Data de Vencimento. Ex.: 2016-03-12">
                </div>

                <div class="input-field">
                    <input type="text" v-model="bill.value" id="value" placeholder="Valor. Somente números!">
                </div>

                <button type="button" @click="submit()" class="btn">Editar</button>
            </form>
        </div>
    </div>
</template>

<style type="text/css">
    .container{
        min-height: 100%;
    }
</style>

<script>
    export default {
        data(){
            return {
                bill: {
                    name: '',
                    date_do: '',
                    value: 0
                }
            };
        },
        ready() {
            let id = this.$route.params.id;
            this.$http.get(`http://billpay.ddns.net/api/bill_pays/${id}`)
                      .then((response) => {
                        this.bill = response.data;
                      })
        },
        methods: {
            submit(){
                this.$http.put(`http://billpay.ddns.net/api/bill_pays/${this.bill.id}`, this.bill)
                          .then((response) => {
                            this.$router.go({name: 'bill-pay.list'});
                            Materialize.toast('Conta Editada com sucesso!', 2500);
                          })
            }
        }
    }
</script>
