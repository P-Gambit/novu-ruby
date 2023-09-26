<div align="center">
  <a href="https://novu.co" target="_blank">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://user-images.githubusercontent.com/2233092/213641039-220ac15f-f367-4d13-9eaf-56e79433b8c1.png">
    <img src="https://user-images.githubusercontent.com/2233092/213641043-3bbb3f21-3c53-4e67-afe5-755aeb222159.png" width="280" alt="Logo"/>
  </picture>
  </a>
</div>

# Novu Ruby client library

[![Gem Version](https://img.shields.io/gem/v/novu.svg)](https://rubygems.org/gems/novu)
[![Gem](https://img.shields.io/gem/dt/novu.svg)](https://rubygems.org/gems/novu/)

> This is a Ruby client library for communicating with the [Novu API](https://api.novu.co/api).

## Installation

You can install the client library via RubyGems:

```ruby
gem install novu
```

Or add it to your Gemfile:

```ruby
gem 'novu'
```

Then run `bundle install`.

## Usage

To use the library, first initialize the client with your API token:

```ruby
require 'novu'

client = Novu::Client.new('YOUR_NOVU_API_TOKEN')
```

If you are using a self-hosted instance of Novu, you can initialize the client with your API token and the URL where your instance is hosted:

```ruby
require 'novu'

client = Novu::Client.new('MY_API_TOKEN', 'http://your-novu-instance')
```

You can then call methods on the client to interact with the Novu API:

```ruby
client.notifications
```

## List of all methods

The client methods map directly to the Novu API endpoints. Here's a list of all the available methods. Check [the API docs](https://docs.novu.co/api/overview) for list of available `methods`.

### Changes

- Get changes: `changes(query = {})`

```ruby
client.changes({
    'page' => 1, # optional
    'limit' => 10, # optional
    'promoted' => 'hello'
})
```

- Get changes count: `count_changes()`

```ruby
client.count_changes()
```
- Apply changes: `apply_bulk_changes()`
```ruby
client.apply_change({
    'changeIds' => ['<insert-all-the-change-ids>']
})
```

- Apply change: `apply_change(change_id)`

```ruby
client.apply_change('7789')
```

### Environments

- Get current environment: `current_environment()`
```ruby
client.current_environment()
```
- Create environment: `create_environment(body)`

```ruby
payload = {
    'name' => 'Staging',
    'parentId' => '7789' # optional
}
client.create_environment(payload)
```

- Get environments: `environments()`

```ruby
client.environments()
```

- Update environment by id: `update_environment(environment_id, body)`

```ruby
client.update_environment('64a713bdexxxxxx', {
    'name' => 'Local', # optional
    'identifier' => 'local', # optional
    'parentId' => '7789', # optional
    'dns' => { # optional
        'inboundParseDomain' => 'dev.test' # optional
    }
})
```

- Get api keys: `api_keys()`

```ruby
client.api_keys()
```

- Regenerate api keys: `regenerate_api_keys()`

```ruby
client.regenerate_api_keys()
```

- `update_widget_settings(body)`

```ruby
client.update_widget_settings({ 'notificationCenterEncryption' => true})
```


### Events

- Trigger event: `trigger_event(body)`

```ruby
payload = {
    'name' => 'Trigger1',
    'payload' => { # optional
        'first-name' => 'Adam' # optional
    },
    'to' => {
        'subscriberId' => '7789'
    },
    'transactionId' => '89kjfke9893' #optional
}
client.trigger_event(payload)
```

- Bulk trigger event: `trigger_bulk_event(body)`

```ruby
payload = {
    'events' => [
        {
            'name' => 'Trigger1',
            'payload' => { # optional
                'first-name' => 'Adam' # optional
            },
            'to' => {
                'subscriberId' => '7789'
            },
            'transactionId' => '89kjfke9893' #optional
        },
        {
            'name' => 'Trigger2',
            'payload' => { # optional
                'last-name' => 'Eve' # optional
            },
            'to' => {
                'subscriberId' => '7789'
            },
            'transactionId' => 'sw900999as' #optional
        }
    ]
}
client.trigger_bulk_event(payload)
```

- Broadcast event to all: `broadcast_event(body)`

```ruby
payload = {
    'name' => 'Trigger',
    'payload' => {
        'first-name' => 'Adam',
        'last-name' => 'Eve'
    },
    'transactionId' => 'sw900999as' #optional
}
client.broadcast_event(payload)
```

- Cancel triggered event: `cancel_triggered_event(transaction_id)`

```ruby
client.cancel_triggered_event('8fxxxee-xxx-4f2b-a0e8-xxxxx')
```


### Execution Details

- Get execution details: `execution_details(query = {})`

```ruby
client.execution_details({
    'notificationId' => '8fxxx-xxx-ef9xxxxce66',
    'subscriberId' => '7789'
})
```

### Feeds

- Create feed: `create_feed(body)`

```ruby
client.create_feed({
    'name' => 'New feed'
})
```

- Get feeds: `feeds()`

```ruby
client.feeds()
```

- Delete feed: `delete_feed(feed_id)`

```ruby
client.delete_feed('xxxx714xxa8cbxxxxx2d932')
```


### Inbound Parse

- Validate the mx record setup for the inbound parse functionality: `validate_mx_record_setup_for_inbound_parse()`

```ruby
client.validate_mx_record_setup_for_inbound_parse()
```

### Integrations

- Get integrations: `integrations()`

```ruby
client.integrations()
```

- Create integration: `create_integration(body)`

```ruby
body = {
    'providerId' => '<insert-provider-id>',
    'channel' => '<insert-channel>',
    'credentials' => {
        # insert all the fields
    },
    'active' => true,
    'check' => true
}
client.create_integration(body)
```

- Get active integrations: `active_integrations()`

```ruby
client.active_integrations()
```

- Get webhook support status for provider: `webhook_provider_status(provider_id)`

```ruby
client.webhook_provider_status('<insert-provider-id>')
```

- Update integration: `update_integration(integration_id, body)`

```ruby
body = {
    'active' => true,
    'check' => true
    'credentials' => {
        # insert all the fields
    },
}
client.update_integration('<insert-provider-id>', body)
```

- Delete integration: `delete_integration(integration_id)`

```ruby
client.delete_integration('<insert-provider-id>')
```

- Get channel limit: `channel_limit(channel_type)`

```ruby
client.channel_limit('<insert-channel-type>')
```

- Get in-app status: `in_app_status()`

```ruby
client.in_app_status()
```


### Layouts

- Layout creation: `create_layout(body)`

```ruby
payload = {
    'name' => 'New layout',
    'content' => '{{{body}}}',
    'variables' => ['<list-variables-here>'], # optional
    'description' => 'This is a description for the new layout', # optional
    'isDefault' => true # optional
}
client.create_layout(payload)
```

- Filter layouts: `layouts(query = {})`

```ruby
client.layouts({
    'page' => 1, # optional
    'pageSize' => 10, # optional
    'sortBy' => 'createdAt', # optional
    'orderBy' => 1 # optional
})
```

- Get layout: `layout(layout_id)`

```ruby
client.layout('<insert-layout-id>')
```

- Delete layout: `delete_layout(layout_id)`

```ruby
client.delete_layout('<insert-layout-id>')
```

- Update a layout: `update_layout(layout_id, body)`

```ruby
payload = {
    'name' => 'Update layout', # optional
    'content' => '{{{body}}}', # optional
    'description' => 'This is a description for the new layout', # optional
    'isDefault' => true # optional
    'variables' => ['<list-variables-here>'], # optional
}
client.update_layout('<insert-layout-id>', payload)
```

- Set default layout: `make_default_layout(layout_id)`

```ruby
client.make_default_layout('<insert-layout-id>')
```


### Messages

- Get messages: `messages(query = {})`

```ruby
payload = {
    'channel' => 'slack', # optional
    'subscriberId' => '7789', # optional
    'transactionId' =>'sw900999as', # optional
    'page' => 4, # optional
    'limit' => 10, # optional
}
client.messages(payload)
```

- Delete message: `delete_message(message_id)`

```ruby
client.delete_message('<insert-message-id>')
```

### Notification Groups

- Create Notification group: `create_notification_group(body)`

```ruby
client.create_notification_group({
    'name' => '<insert-name>'
})
```

- Get Notification groups: `notification_groups()`

```ruby
client.notification_groups()
```

### Notification Templates

- Get notification templates: `notification_templates(query = {})`

```ruby
client.notification_templates({
    'page' => 4, # optional
    'limit' => 10, # optional
})
```

- Create notification template: `create_notification_template(body)`

```ruby
body = {
    'name' => '<insert-name>',
    'notificationGroupId' => 'notificationGroupId',
    'tags' => ['tags'], # optional
    'description' => 'description', # optional
    'steps' => [ # optional
       # insert all fields here
    ], 
    'active' => true, # optional
    'draft' => true, # optional
    'critical' => true, # optional
    'preferenceSettings' => { # optional
       # insert all fields here
    },
    'blueprintId' => 'blueprintId' # optional
}
client.create_notification_template(body)
```

- Update notification template: `update_notification_template(template_id, body)`

```ruby
body = {
    'name' => '<insert-name>',
    'notificationGroupId' => 'notificationGroupId',
    'tags' => ['tags'], # optional
    'description' => 'description', # optional
    'steps' => [ # optional
       # insert all fields here
    ], 
    'active' => true, # optional
    'draft' => true, # optional
    'critical' => true, # optional
    'preferenceSettings' => { # optional
       # insert all fields here
    },
    'blueprintId' => 'blueprintId' # optional
}
client.update_notification_template('<insert-template-id>', body)
```

- Delete notification template`delete_notification_template(template_id)`

```ruby
client.delete_notification_template('<insert-template-id>')
```

- Get a notification template: `notification_template(template_id)`

```ruby
client.notification_template('<insert-template-id>')
```

- Get a notification template blueprint: `notification_template_blueprint(template_id)`

```ruby
client.notification_template_blueprint('<insert-template-id>')
```

- Create a new notification template blueprint: `create_notification_template_blueprint(template_id)`

```ruby
client.create_notification_template_blueprint('<insert-template-id>')
```

- Update notification template status: `update_notification_template_status(template_id, body)`

```ruby
client.update_notification_template_status('<insert-template-id>', { 'active' => true })
```

### Notification

- Get notifications: `notifications(query = {})`

```ruby
body = {
    'channels' => ['<insert-channels>'],
    'templates' => ['<insert-templates>'],
    'emails' => ['<insert-emails>'],
    'search' => '<insert-search-string>'
    'page' => 2 , # optional
    'transactionId' =>'sw900999as', # optional
}
client.notifications(body)
```

- Get notification statistics: `notifications_stats()`

```ruby
client.notifications_stats()
```

- Get notification graph statistics: `notifications_graph_stats(query = {})`

```ruby
client.notifications_graph_stats({
    'days' => 5 # optional
})
```

- Get notification: `notification(notification_id)`

```ruby
client.notification('<insert-notification-id>')
```

### Subscribers

- Get subscribers: `subscribers(query = {}) `

```ruby
client.subscribers({
    'page' => 1, # optional
    'limit' => 15, # optional
})
```

- Create subscriber: `create_subscriber(body)`

```ruby
payload = {
    'subscriberId' => '7789',
    'email' => '<insert-email>', # optional
    'firstName' => '<insert-firstName>', # optional
    'lastName' => '<insert-lastName>', # optional
    'phone' => '<insert-phone>', # optional
    'avatar' => '<insert-profile-avatar>' # optional
}
client.create_subscriber(payload)
```

- `subscriber(subscriber_id)`

```ruby
client.subscriber('<insert-subscriber-id>')
```

- Update subscriber: `update_subscriber(subscriber_id, body)`

```ruby
payload = {
    'email' => '<insert-email>', # optional
    'firstName' => '<insert-firstName>', # optional
    'lastName' => '<insert-lastName>', # optional
    'phone' => '<insert-phone>', # optional
    'avatar' => '<insert-profile-avatar>' # optional
}
client.update_subscriber('<insert-subscriber-id>', payload)
```

- Delete subscriber: `delete_subscriber(subscriber_id)`

```ruby
client.delete_subscriber('<insert-subscriber-id>')
```

- Update subscriber credentials: `update_subscriber_credentials(subscriber_id, body)`

```ruby
body = {
    'providerId' => '<insert-provider-id>',
    'credentials' => {
        # Insert all fields here 
    } 
}
client.update_subscriber_credentials('<insert-subscriber-id>', body)
```

- Update subscriber online status: `update_subscriber_online_status(subscriber_id, body)`

```ruby
client.update_subscriber_online_status('<insert-subscriber-id>', { 'isOnline' => true })
```

- Get subscriber preferences: `subscriber_preferences(subscriber_id)`

```ruby
client.subscriber_preferences('<insert-subscriber-id>')
```

- Update subscriber preference: `update_subscriber_preference(subscriber_id, template_id, body)`

```ruby
body = {
    'channel' => {
        # Insert all fields here
    },
    'enabled' => true
}
client.update_subscriber_preference('<insert-subscriber-id>', '<insert-template-id>', body)
```

- Get in-app notification feed for a particular subscriber: `subscriber_notification_feed(subscriber_id, query = {})`

```ruby
client.subscriber_notification_feed('<insert-subscriber-id>', {
    'page' => 3, # optional
    'limit' => 15, # optional
    'read' => true, # optional
    'seen' => true, # optional
})
```

- Get the unseen in-app notifications count for subscribers feed: `subscriber_unseen_notification_count(subscriber_id, query = {})`

```ruby
client.subscriber_unseen_notification_count('<insert-subscriber-id>', {
    'limit' => 15, # optional
    'seen' => false, # optional
})
```

- Mark a subscriber feed message as seen: `mark_subscriber_feed_seen(subscriber_id, body)`

```ruby
client.mark_subscriber_feed_seen('<insert-subscriber-id>', {
    'messageId' => '<insert-message-id>',
    'mark' => {
        'seen' => true,
        'read' => true
    }
})
```

- Mark message action as seen: `mark_message_action_seen(subscriber_id, message_id, type)`

```ruby
client.mark_message_action_seen('<insert-subscriber-id>', '<insert-message-id>', '<insert-type>')
```

### Tenants

- Tenant create: `create_tenant(body)`

```ruby
client.create_tenant({
    'identifier' => '<a-unique-identifier>',
    'name' => '<name-of-the-tenant>',
    'data' => {
        'company' => 'a company',
        'date-registered' => '2023-0-15'
    }
})
```

- Get tenants: `tenants(query = {})`

```ruby
client.tenants({
    'page' => 1, # optional
    'limit' => 10, # optional
})
```

- Get tenant: `tenant(identifier)`

```ruby
client.tenant('<a-unique-identifier>')
```

- Update tenant: `update_tenant(identifier, body)`

```ruby
client.update_tenant('<a-unique-identifier>', {
    'identifier' => '<a-unique-identifier>',
    'name' => '<name-of-the-tenant>',
})
```

- Delete tenant: `delete_tenant(identifier)`

```ruby
client.delete_tenant('<a-unique-identifier>')
```

### Topics

- Topic creation: `create_topic(body)`

```ruby
client.create_topic({
    'key' => 'key',
    'name' => 'name'
})
```

- Filter topics: `topics(query = {})`

```ruby
client.topics({
    'name' => 'name', # optional
    'page' => 1, # optional
    'pageSize' => 10, # optional
})
```

- Subscribers addition: `add_subscribers(topic_key, body)`

```ruby
client.add_subscribers('<insert-topic-key>', {
    'subscribers' => ['<insert-list-of-subscribers>']
})
```

- `remove_subscribers(topic_key, body)`

```ruby
client.
```

- Get topic: `topic(topic_key)`

```ruby
client.topic('<insert-topic-key>')
```

- Rename a topic: `rename_topic(topic_key, body)`

```ruby
client.rename_topic('<insert-topic-key>', {
    'name' => 'new name'
})
```

### For more information about these methods and their parameters, see the [API documentation](https://docs.novu.co/api-reference).

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/novuhq/novu-ruby
