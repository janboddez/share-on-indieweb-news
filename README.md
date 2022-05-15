# Share on IndieNews
Automatically submit WordPress posts to [IndieNews](https://news.indieweb.org/).

In your theme (or elsewhere), use `get_post_meta( $post->ID, '_share_on_indienews_url', true )` to retrieve the resulting syndication URL.

There's no options page, but you can change the language-specific endpoint using the `share_on_indienews_default_url` filter, e.g.:
```
add_filter( 'share_on_indienews_default_url' , function( $default_url ) {
  return 'https://news.indieweb.org/de';
} );
```
If you want to display the sharing option for post types other than `post` and `page`, there's `share_on_indienews_post_types`:
```
add_filter( 'share_on_indienews_post_types' , function( $post_types ) {
  $post_types[] = 'my_custom_post_type_slug';

  return $post_types;
} );
```
Sharing can be made opt-in:
```
add_filter( 'share_on_indienews_optin', '__return_true' );
```
Or automated, based on, e.g., the presence of an "IndieWeb" tag:
```
add_filter( 'share_on_indienews_enabled', function( $is_enabled, $post ) {
  if ( $post->has_tag( 'indieweb' ) ) {
    return true;
  }

  return $is_enabled;
}, 10, 2 );
```
