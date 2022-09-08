# Calendar Resource Management
This app enables the 🗓️ [Calendar](https://github.com/nextcloud/calendar) App to work with resources and rooms

## Installation

### Obtain the latest pre-release build

Builds are available at https://github.com/nextcloud-releases/calendar_resource_management/releases.

Download and extract `calendar_resource_management.tar.gz` into `nextcloud/apps/`.

### Activate it within the apps menu

## Configuration

`*` denotes a required argument  
All boolean fields default to null if not specified

| Command  | Description | Parameters  | Associated Table | Notes |
|---|---|---|---|---|
| calendar-resource:building:create | Create a building resource |`display_name`* `address` `description` `wheelchair_accessible`| `calresources_building` | |
| calendar-resource:story:create | Create a story resource | `display_name` `building_id` | `calresources_stories` | Needs an associated building id |
| calendar-resource:room:create | Create a room resource | `story_id`* `uid`* `display_name`* `email`* `room_type`* `contact_person_user_id` `capacity` `room_number` `has_phone` `has_video_conferencing` `has_tv` `has_projector` `has_whiteboard` `wheelchair_accessible` | `calresources_rooms` | Needs an associated story id |
| calendar-resource:restriction:create | Create a restriction on a resource | `entity_type`* `entity_id`* `group_id`*  | `calresources_restricits` | This restricts a resource to a group |
| calendar-resource:resource:create | Create a general resource | `uid`* `building_id`* `display_name`* `email`* `resource_type`* `contact_person_user_id` | `calresources_resources` | Needs an associated building id |
| calendar-resource:vehicle:create | Create a vehicle resource | `uid`* `building_id`* `display_name`* `email`* `contact_person_user_id`* `vehicle_type`* `vehicle_make`* `vehicle_model`* `is_electric` `range` `seating_capacity` | `calresources_vehicles` | Needs an associated building id |
| calendar-resource:resources:list | List all resources | | | |
| calendar-resource:resource:delete | Delete a resource and anything that belongs to them | `resource_type`* `id`* | | |

### Example for creating a room

```
php occ calendar-resource:building:create "SpaceZ office Berlin" "Testweg 23, 12345 Berlin, Germany" ""
php occ calendar-resource:story:create 1 "2nd floor"
php occ calendar-resource:room:create 1 "berlin_main_office" "Shared office" "room.berlin.main@spacexyz.com" 0 "demouser" 25 201
```

The resources will be added to the calendar app via cron.

Any create command will return the ID of the created resource as the last line.






