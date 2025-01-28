### Data Dictionary for `roles` Table

| **Data Element Name** | **Data Type** | **Description** | **Length/Size** | **Constraints/Rules** | **Default Value** | **Source** | **Relationships** | **Permissions/Access** | **Examples** |
|----------------------|-------------|----------------|---------------|------------------|---------------|--------|--------------|-----------------|----------|
| `id` | `ObjectId` | Unique identifier for the role (primary key). | 24 bytes | Primary key, unique | Auto-generated | System | - | Read/Write (Admin) | `60d21b4667d0d8992e610c85` |
| `communityId` | `ObjectId` | Reference to the associated community. | 24 bytes | Foreign Key referencing `communities.id` | - | System | Many-to-One (Community → Roles) | Read/Write (Admin) | `60d21b4667d0d8992e610c90` |
| `name` | `String` | Name of the role (e.g., Admin, Moderator). | 255 characters | Unique within a community, required | - | User Input | - | Read/Write (Admin) | `"Moderator"` |
| `color` | `Int` | Color code associated with the role (stored as an integer). | 4 bytes | Should be a valid RGB or HEX representation | `16777215` (white) | User Input | - | Read/Write (Admin) | `16711680` (Red) |
| `permissions` | `Int` | Bitwise integer representing permissions. | 4 bytes | Should be a valid bitwise permission integer | `0` | System | - | Read/Write (Admin) | `755` |
| `mentionable` | `Boolean` | Whether the role is mentionable in discussions. | 1 byte | `true` or `false` | `false` | User Input | - | Read/Write (Admin, Moderator) | `true` |
| `createdAt` | `DateTime` | Timestamp when the role was created. | 8 bytes | Auto-generated at creation | Current timestamp | System | - | Read (Admin) | `2024-01-28T12:00:00Z` |
| `updatedAt` | `DateTime` | Timestamp when the role was last updated. | 8 bytes | Auto-updated on modification | Current timestamp | System | - | Read (Admin) | `2024-01-29T14:30:00Z` |
