<template>
    <nav class="light-blue lighten-1" role="navigation">
        <div class="nav-wrapper container">
          <a id="logo-container" href="#" class="brand-logo">BillPays</a>
          <ul class="right hide-on-med-and-down">
            <li v-for="o in links">
                <a v-link="{name: o.routeName}">{{ o.label }}</a>
            </li>
        </ul>

        <ul id="nav-mobile" class="side-nav">
            <li v-for="o in links">
                <a v-link="{name: o.routeName}">{{ o.label }}</a>
            </li>
        </ul>

        <a href="#" data-activates="nav-mobile" class="button-collapse">
            <i class="material-icons">menu</i>
        </a>
    </div>
    </nav>

    <router-view></router-view>

    <footer class="page-footer orange">
        <div class="container">
          <div class="row">
            <div class="col l6 s12">
              <h5 class="white-text">Bill Pays</h5>
              <p class="grey-text text-lighten-4">
                Sistemas de controle de contas a pagar.
              </p>


          </div>
          <div class="col l3 s12">
              <h5 class="white-text">Settings</h5>
              <ul>
                <li><a class="white-text" href="#!">Link 1</a></li>
            </ul>
        </div>
        <div class="col l3 s12">
          <h5 class="white-text">Connect</h5>
          <ul>
            <li><a class="white-text" href="#!">Link 1</a></li>
        </ul>
    </div>
    </div>
    </div>
    <div class="footer-copyright">
      <div class="container">
          Made by <a class="orange-text text-lighten-3" href="http://materializecss.com">Materialize</a>
      </div>
    </div>
    </footer>
</template>

<script>
    export default {
        data(){
            return {
                links: [
                    {label: 'Contas a pagar', routeName: 'bill-pay.list'},
                ]
            };
        },
        created() {
          Echo.channel('my-channel')
              .listen('BillPayCreated', (e) => {
                let bill = e.billPay;
                Materialize.toast(' Nova Conta Cadastrada.' +
                                  ' Nome: ' + bill.name +
                                  ' | Vencimento: ' + bill.date_do +
                                  ' | Valor: R$ ' + bill.value, 4000);
              })
            $(function(){
                $('.button-collapse').sideNav();
            });
        }
    }
</script>
