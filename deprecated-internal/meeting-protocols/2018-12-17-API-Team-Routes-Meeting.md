## Basic team routes

The api should provide following routes:

- `GET /teams`  
  - args: `none`  
  - response: `{ "teams": [{ "id": "<uuid>", "name": "My Team" }, ...] }`
- `POST /teams`   
  - args: `{ "name": "My Team" }`  
  - response: `{ "id": "<uuid>", "name": "My Team" }`
- `GET /teams/:id`
  - args: `none`  
  - response: `{ "id": "<uuid>", "name": "My Team" }`
- `PUT /teams/:id`
  - args: `{ "name": "New Team Name" }` (and consider following updatable properties)
  - response: `{ "id": "<uuid>", "name": "New Team Name" }`


## Supporting teams on images routes

Routes to consider updating to support teams:

- `GET /images`
- `POST /images`
- ...all other images routes

There are two options to implement team support:

- Option 1: `/teams/:id/images`  
- Option 2: `/images` with property `team_id` in json body or as GET url param

**We are deciding for Option 2!**

We are disallowing using the `GET/POST /images` without a `team_id` property.  
Actions on a single image (`GET/PUT/PATCH /images/:id`) do not require a `team_id` property.
