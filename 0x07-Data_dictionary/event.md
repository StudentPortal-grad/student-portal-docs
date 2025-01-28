## Data Dictionary: Events Table

| Data Element Name  | Data Type   | Description | Length/Size | Constraints/Rules | Default Value | Source | Relationships | Permissions/Access | Examples |
|--------------------|------------|-------------|-------------|------------------|---------------|--------|--------------|------------------|----------|
| id                | ObjectId   | Unique identifier for the event | 24 chars | Primary Key, Unique | Auto-generated | System | Primary key, referenced in `recommendations`, `attendees`, `RSVPs.eventId` | Admin, Event Creator | `656a3f1e8bfa9c001f3b2d6c` |
| title             | String     | Name of the event | 255 chars | Required | None | User Input | No direct relationships | Admin, Event Creator | "AI Workshop" |
| description       | String     | Detailed description of the event | 1000 chars | Optional | None | User Input | No direct relationships | Admin, Event Creator | "A workshop about AI advancements." |
| dateTime         | DateTime   | Date and time when the event occurs | N/A | Required | None | User Input | Indexed (`event_date_time_index`) | Admin, Event Creator | `2025-03-15T10:00:00Z` |
| location         | String     | Physical or virtual location | 255 chars | Optional | None | User Input | No direct relationships | Admin, Event Creator | "Zoom Meeting" or "Conference Hall A" |
| capacity         | Number     | Maximum number of attendees allowed | Integer (32-bit) | Optional | None | User Input | No direct relationships | Admin, Event Creator | `100` |
| visibility       | String     | Visibility of the event | 10 chars | Enum(`public`, `private`, `community`) | `public` | User Input | Related to `communityId` for filtering | Admin, Event Creator | "public" |
| attendees        | ObjectId[] | List of users who have RSVP'd | Array of ObjectIds (24 chars each) | References `RSVPs.id` | Empty Array | System | Foreign Key (`RSVPs.userId`) | Admin, Event Creator | `['656a3f1e8bfa9c001f3b2d6d', '656a3f1e8bfa9c001f3b2d6e']` |
| creatorId        | ObjectId   | User who created the event | 24 chars | Required | None | System | Foreign Key (`users.id`) | Admin, Event Creator | `656a3f1e8bfa9c001f3b2d6f` |
| status           | String     | Current status of the event | 15 chars | Enum(`upcoming`, `ongoing`, `completed`, `cancelled`) | `upcoming` | System | No direct relationships | Admin, Event Creator | "upcoming" |
| recommendations  | ObjectId[] | Suggested related events | Array of ObjectIds (24 chars each) | Optional | Empty Array | System | Foreign Key (`events.id` - self-referencing) | Admin, Event Creator | `['656a3f1e8bfa9c001f3b2d70']` |
| communityId      | ObjectId   | Community hosting the event | 24 chars | Optional | None | User Input | Foreign Key (`communities.id`) | Admin, Event Creator | `656a3f1e8bfa9c001f3b2d71` |
| createdAt        | DateTime   | Timestamp of event creation | N/A | Auto-generated | Current Timestamp | System | No direct relationships | Admin, Event Creator | `2025-01-20T12:00:00Z` |
| updatedAt        | DateTime   | Timestamp of last update | N/A | Auto-updated | Current Timestamp | System | No direct relationships | Admin, Event Creator | `2025-01-22T14:00:00Z` |


