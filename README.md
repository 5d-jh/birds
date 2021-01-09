# Types
## Primitives
* `<string>`
* `<number:int>`
* `<number:double>`
* `<primary_index:(entity_name)>`
* `<date>`

## ReplyScope
```json
["everyone", "users_i_follow", "me"]
```

## Topic
```json
{
    "id": "<primary_index:Topic>",
    "text": "<string>",
    "created_at": "<date>"
}
```

# API Reference
## Create a user
### Request
* Method: `POST`
* Path: `/users`
```json
{
    "username": "<string>",
    "password": "<string>",
    "email": "<string>"
}
```

### Response
* Status Code: `201`

## Get users
### Request
* Method: `GET`
* Path: `/users`
* Query Parameter
    * `following`: `<primary_index:User>`
    * `followed_by`: `<primary_index:User>`

### Response
* Status Code: `201`
* Body:
```json
{
    "users": [
        {
            "username": "<string>",
            "password": "<string>",
            "email": "<string>",
            "followings_count": "<number:int>",
            "followers_count": "<number:int>"
        }
    ]
}
```

## Create a token
### Request
* Method: `POST`
* Path: `/token`
* Body:
```json
{
    "client_id": "<primary_index:Client>",
    "user_id": "<primary_index:User>",
    "password": "<string>"
}
```
### Response
* Status code: `201`
* Body:
```json
{
    "access_token": "<string>",
    "refresh_token": "<string>",
}
```

## Create a post
### Request
* Method: `POST`
* Path: `/users/:user_id/posts`
* Body:
```json
{
    "text": "<string>",
    "reply_scope": "<ReplyScope>",
    "topics": ["<Topic>"],
    "replying_to": "<primary_index:Post?>"
}
```
### Response
* Status Code: `201`

## Get posts
### Request
* Method: `GET`
* Path: `/posts`
* Query Parameters
    * `user_id`: `<primary_index:User?>`
    * `topic`: `<primary_index:Topic?>`

### Response
```json
{
    "posts": [
        "id": "<primary_index:Post>",
        "text": "<string>",
        "reply_scope": "<ReplyScope>",
        "topics": "<Topic>"
    ]
}
```

## Get replies
### Request
* Method: `GET`
* Path: `/posts/:post_id`
* Query Parameter
    * `page`: `<number:int>`
    * `size`: `<number:int>`

### Response
* Status Code: `201`
* Body:
```json
{
    "replies": [
        {
            "id": "<primary_index>",
            "text": "<string>",
            "reply_scope": "<ReplyScope>",
            "topics": ["<Topic>"]
        }
    ]
}
```

## Get topics
### Request
* Method: `GET`
* Path: `/topics`

### Response
* Status Code: `201`
* Body:
```json
{
    "topics": [
        {
            "id": "<primary_index>",
            "created_at": "<date>",
            "text": "<string>",
            "mentioned_count": "<number:int>"
        }
    ]
}
```
