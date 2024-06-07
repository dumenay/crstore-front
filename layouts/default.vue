<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer
        expand-on-hover
        rail
        theme="dark"
      >
        <v-list>
          <v-list-item
            prepend-avatar="https://pbs.twimg.com/media/EiJaqcCWAAAgckA.jpg"
            subtitle="nobru@loud.com"
            title="Xapeleta"
          ></v-list-item>
        </v-list>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item to="/" prepend-icon="mdi-home" title="Home" value="home"></v-list-item>
          <v-list-item to="/users" prepend-icon="mdi-card-account-details" title="Users" value="users"></v-list-item>
          <v-list-item to="/categories" prepend-icon="mdi-view-list" title="Categories" value="categories"></v-list-item>
          <v-list-item to="/products" prepend-icon="mdi-food" title="Products" value="products"></v-list-item>
          <v-list-item to="/coupons" prepend-icon="mdi-ticket-percent" title="Coupons" value="coupons"></v-list-item>
          <v-list-item to="/orders" prepend-icon="mdi-tag-plus" title="Orders" value="orders"></v-list-item>
          <v-list-item to="/ordersProducts" prepend-icon="mdi-food-fork-drink" title="Orders Products" value="ordersProducts"></v-list-item>
          <v-list-item to="/payments" prepend-icon="mdi-cash-multiple" title="Payments" value="payments"></v-list-item>
        </v-list>
      </v-navigation-drawer>
      <v-main style="height: 100vh; background-color: black;" theme="dark">

        <slot/>

      </v-main>
    </v-layout>
  </v-card>
</template>

<script>
export default {
  name: 'default'
}
</script>
