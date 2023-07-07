# WP_WooThankYouPageRedirectBaseOnProductID
WordPress woocommerce redirect thank you page base on product ID

```PHP

add_action( 'woocommerce_thankyou', 'bba_action_woocommerce_thankyou', 10, 1 );
function bba_action_woocommerce_thankyou( $order_id ) {

  if( ! $order_id ) {
      return;
  }

  // Instannce of the WC_Order Object
  $order = wc_get_order( $order_id ); 

  // Is a WC_Order
  if ( is_a( $order, 'WC_Order' ) ) {
      // False
      $redirection = false;
      
      // Loop through order items
      foreach ( $order->get_items() as $item_key => $item ) {
          // Product ID(s)
          $product_ids = array( $item->get_product_id(), $item->get_variation_id() );
          
          // Product ID in array
          // This case NOT or aside to these product ID then the rest redirect to TY page 2
          if ( !in_array( 16457, $product_ids ) || !in_array( 16444, $product_ids ) ) { $redirection = true; }
      }
  }

  // Make the custom redirection when a targeted product has been found in the order
  if ( $redirection ) {
      wp_safe_redirect( home_url( '/thank-you-enroled/' ) );
      exit;
  }
}

```

Source: 

https://stackoverflow.com/questions/65038847/thank-you-page-redirection-for-specific-product-id-in-woocommerce-order-items
