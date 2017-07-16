# If you want to display welcome message or redirect the user to any page when the user login for the first time only.
# Use below functions in your activated theme's functions.php

//Whenever a new user is created, this function will add a custom field with value 1.
function function_new_user($user_id) { 
   add_user_meta( $user_id, '_new_user', '1' );
}
add_action( 'user_register', 'function_new_user');

//The next function will check if it's the first login and redirect the user.
function function_check_login_redirect($user_login, $user) {
   $logincontrol = get_user_meta($user->ID, '_new_user', 'TRUE');
   if ( $logincontrol ) {
      //set the user to old
      update_user_meta( $user->ID, '_new_user', '0' );

      //Do the redirects or whatever you need to do for the first login
      wp_redirect( 'http://www.example.com', 302 ); exit;
   }
}
add_action('wp_login', 'function_check_login_redirect', 10, 2);

# Tip: The function_check_login_redirect knows the user. You can even offer the user a custom info or call to action.
