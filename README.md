# Telegram JSON data strcut

https://github.com/vysheng/tg/blob/master/json-tg.c

## Peer

`json_pack_peer()`

```
{
  id: 0
  type: "" // user | chat | encr_chat `json_pack_peer_type()`
  print_name: ""
  flags: 0
  <User | Chat | Encr Chat>
}
```

* User `json_pack_user()`

    ```
    {
      first_name: ""
      last_name: ""
      real_first_name: ""
      real_last_name: ""
      phone: ""
      username: ""
    }
    ```

* Chat `json_pack_chat()`

    ```
    {
      title: ""
      admin: <User>
      members_num: 0
      members: [{
        <User>
        inviter: <User>
      }]
    }
    ```

* Encr Chat `json_pack_encr_chat()`

    ```
    {
      user: <User>
    }
    ```

## Message

`json_pack_message()`

```
{
  id: 0
  flags: 0
  fwd_from: <Peer>
  fwd_date: 0
  reply_id: 0
  mention: true
  from: <Peer>
  to: <Peer>
  out: false
  unread: false
  service: false
  date: 0
  text: ""
  media: <Media>
  action: <Service>
  event: "" // message | service | read `json_pack_read()`
}
```

## UserStatus

`json_pack_user_status()`

```
{
  event: "online-status"
  user: <Peer>
  online: true
  state // 1 | 0 | -1 | -2 | -3 | -4
  when: ""
}
```

when:

* `YYYY-MM-DD HH:mm:ss` state > 0 || state == -1
* `long time ago` state == 0
* `recently` state == -2
* `last week` state == -3
* `last month` state == -4

## Update

`json_peer_update()` https://github.com/vysheng/tg/blob/master/interface.c

```
{
  event: "updates"
  peer: <Peer>
  updates: [""] // `json_pack_updates()`
}
```

updates:

* created
* deleted
* phone
* contact
* photo
* blocked
* real_name
* name
* requested
* working
* flags
* title
* admin
* members
* username

## Media

`json_pack_media()`

```
{
  type: "" // unsupported | photo | document | geo | contact | webpage | venue | ???
  // photo
  caption: ""
  // geo
  longitude: 0.0
  latitude: 0.0
  // contact
  phone: ""
  first_name: ""
  last_name: ""
  user_id: 0
  // webpage
  url: ""
  title: ""
  description: ""
  author: ""
  // venue
  longitude: 0.0
  latitude: 0.0
  title: ""
  address: ""
  provider: ""
  venue_id: ""
}
```

## Typing

`json_pack_typing()`

```
{
  status: ""
}
```

status:

* doing nothing
* typing
* deleting typed message
* recording video
* uploading video
* recording audio
* uploading audio
* uploading photo
* uploading document
* choosing location
* choosing contact
* ???

## Service

`json_pack_service()`

```
{
  type: ""
  // chat_created | chat_rename
  title: ""
  // chat_add_user | chat_add_user_link | chat_del_user
  user: <Peer User>
  // set_ttl
  ttl: 0
  // read | delete | screenshot
  count: 0
  // notify_layer
  layer: 0
  // typing
  <Typing>
}
```

type:

* geo_created
* geo_checkin
* chat_created
* chat_rename
* chat_change_photo
* chat_delete_photo
* chat_add_user
* chat_add_user_link
* chat_del_user
* set_ttl
* read
* delete
* screenshot
* flush
* resend
* notify_layer
* typing
* noop
* request_key
* accept_key
* commit_key
* abort_key
* ???
