Admin Notes are meant for displaying insightful information about your WooCommerce store, extensions, activity, and achievements. They’re also useful for displaying information that can help with the day-to-day tasks of managing and optimizing a store.

### Define the Activation Logic

```php
$data_store = WC_Data_Store::load('admin-note');
```

Before creates any new notes, it’s a good practice to first check for any existing notes of the same type. This helps us make sure we’re not creating duplicate notes, which can cause clutter and confusion for merchants.

```php
$note_ids = $data_store->get_notes_with_name( self::NOTE_NAME );
  foreach( (array) $note_ids as $note_id ) {
    $note           = Notes::get_note( $note_id );
    $content_data   = $note->get_content_data();
    if ( property_exists( $content_data, 'getting_started' ) ) {
      return;
    }
  }
```

Here we’re querying the Admin Note records in the Data Store for any with a name that matches our note name. If there are any matches with a property in their `content_data` called `getting_started`, we’ll bail out. This means that our note type already exists. We’ll go over `content_data` in more detail just a bit later.

Next, let’s write a bit of logic to generate some of the content that our Admin Note will display. Our example shows the time that our extension was activated, but that’s just one simple example of countless use cases.

```php
$activated_time = current_time( 'timestamp', 0);
$activated_time_formatted = date( 'F jS', $activated_time );
```

Let’s instantiate a new Admin Note object so we can start tailoring its properties and content:

```php
$note = new Note();
```

With our new Admin Note object instantiated, we’ll start by setting its title property:

```php
$note->set_title( 'Getting Started' );
```

Next, we’ll use some of the variables we created earlier to populate our note’s content:

```php
$note->set_content(
  sprintf(
    'Extension activated on %s.', $activated_time_formatted
  )
);
```

In addition to content, Admin Notes also support structured content. You can use the `content_data` property for all sorts of things. It is backed by a `longtext` column in the database.

```php
$note->set_content_data( (object) array(
   'getting_started'       => true,
   'activated'             => $activated_time,
   'activated_formatted'   => $activated_time_formatted
) );
```

Next, let’s set the note’s `type` property. Note types are defined as enum-style class constants in the Note class. Available note types are _error_, _warning_, _update_, _info_, and _marketing_. When selecting a note type, be aware that the _error_ and _update_ result in the note being shown as a Store Alert, not in the Inbox. It’s best to avoid using these types of notes unless you absolutely need to.

We’ll use an info type for our note:

```php
$note->set_type( Note::E_WC_ADMIN_NOTE_INFORMATIONAL );
```

Admin Notes also support a few different layouts. You can specify `banner`, `plain`, or `thumbnail` as the layout. If you’re interested in seeing the different layouts in action, @fermarichal coded [a simple plugin](https://gist.github.com/octaedro/864315edaf9c6a2a6de71d297be1ed88) that you can install to experiment with them.

We’ll choose `plain` as our layout, but it’s also the default, so we could leave this property alone and the effect would be the same:

```php
$note->set_layout( 'plain' );
```

If we have an image that we want to add to our Admin Note, we can specify it here as well. This property ultimately renders as the `src` attribute on an `img` tag, so use a string here.

```php
$note->set_image( '' );
```

Next, we’ll set the values for our Admin Note’s `name` and `source` properties. As a best practice, you should store your extension’s name (slug) in the `source` property of the note. You can use the `name` property to support multiple sub-types of notes. This gives you a handy way of namespacing your notes and managing them at both a high and low level.

```php
$note->set_source( 'admin-note-example');
$note->set_name( self::NOTE_NAME );
```

Admin Notes can support 0, 1, or 2 actions (buttons). You can use these actions to capture events that trigger asynchronous processes or help the merchant navigate to a particular view to complete a step, or even simply to provide an external link for further information.

```php
$note->add_action(
  'settings', 'Open Settings', '?page=wc-settings&tab=general'
);
$note->add_action(
  'learn_more', 'Learn More', 'https://example.com'
);
```

Once we’re satisfied with the properties on our Admin Note, we need to save it to make sure those values are written to the database:

```php
$note->save();
```

### Define Deactivation Logic

As a best practice, extensions that use Admin Notes should clean up behind themselves when the merchant deactivates them by deleting any notes they created. Let’s fill in the details of our `remove_activity_panel_inbox_welcome_notes()` function to do that:

```php
public static function remove_activity_panel_inbox_welcome_notes() {
  if ( ! class_exists( 'Automattic\WooCommerce\Admin\Notes\Notes' ) ) {
    return;
  }
  Notes::delete_notes_with_name( self::NOTE_NAME );
}
```

### Database
**Storage Tables**:
- **wp_wc_admin_notes**: This table stores all the admin notes. Each note typically includes information such as the note content, the type of note (info, warning, error), and timestamps related to its creation and display.
- **wp_wc_admin_note_actions**: This table stores actions (buttons) associated with admin notes. 
**Fields**:
- **wp_wc_admin_notes**
	- **note_id**: Unique identifier for each admin note.
	- **name**: Name or title of the admin note.
	- **type**: Type of note (e.g., 'info', 'warning', 'error').
	- **locale**: Locale or language context for the note (optional).
	- **content**: Main content or message of the note.
	- **icon**: Optional icon associated with the note (for visual differentiation).
	- **status**: Status of the note (e.g., 'unactioned', 'actioned', 'dismissed').
	- **is_dismissible**: Boolean indicating if the note can be dismissed by the user.
	- **dismissible_after**: Date or condition after which the note can be dismissed.
	- **created_date**: Date when the note was created.
	- **modified_date**: Date when the note was last modified.
	- **action_links**: Optional links or actions associated with the note (stored as serialized data).
- **wp_wc_admin_note_actions**
	- **action_id**: Unique identifier for each action associated with an admin note.
	- **note_id**: Foreign key linking to the `wp_wc_admin_notes` table.
	- **name**: Name or label for the action (e.g., 'Dismiss', 'View').
	- **url**: Optional URL associated with the action.
	- **query**: Optional query parameters for the action URL.
	- **is_primary**: Boolean indicating if the action is the primary action for the note.
	- **query_args**: Serialized data for additional query arguments associated with the action.

### Usage Explanation
- **Admin Notes**: These fields store information about each admin note, including its content, type, status, and associated actions. Notes are used to communicate important information or tasks to store administrators.
- **Note Actions**: These fields store details about actions that can be taken in response to an admin note, such as dismissing the note or navigating to related pages. Each action is linked to a specific note through the `note_id` field.

## Resource
- [Using the Admin Notes Inbox in WooCommerce](https://developer.woocommerce.com/2020/10/16/using-the-admin-notes-inbox-in-woocommerce/)
