### Data Dictionary for `roles` Table

| **Data Element Name** | **Data Type**  | **Description**                                     | **Length/Size** | **Constraints/Rules**            | **Default Value** | **Source**  | **Relationships**                        | **Permissions/Access** | **Examples** |
|----------------------|---------------|----------------------------------------------------|---------------|--------------------------------|-----------------|------------|--------------------------------|--------------------|------------|
| `id`                | `ObjectId`     | Unique identifier for the role (primary key).     | 24 bytes      | Primary key, unique, auto-generated | Auto-generated  | System     | Referenced in `users.roles`          | Read (Public), Write (Admin) | `"507f1f77bcf86cd799439500"` |
| `communityId`       | `ObjectId`     | ID of the community this role belongs to.        | 24 bytes      | Foreign key, references `communities.id` | Required        | System     | References `communities.id`          | Read (Public), Write (Admin) | `"507f1f77bcf86cd799439100"` |
| `name`              | `String`       | Name of the role (e.g., `Admin`, `Moderator`).   | 100 chars     | Required, unique within community | Required        | User input  | -                                    | Read (Public), Write (Admin) | `"Moderator"` |
| `color`             | `Int`          | Color code for the role.                         | 4 bytes       | Must be a valid RGB integer    | Optional        | User input  | -                                    | Read (Public), Write (Admin) | `16711680` (`#FF0000` - Red) |
| `permissions`       | `Int`          | Bitwise integer representing multiple permissions. | 4 bytes       | Must be a valid bitwise value   | Required        | System      | -                                    | Read (Admin), Write (Admin) | `7` (Role has permission : `READ + WRITE + DELETE`) |
| `mentionable`       | `Boolean`      | Whether the role is mentionable in discussions. | 1 byte        | Default: `false`                | `false`         | User input  | -                                    | Read (Public), Write (Admin) | `true` |
| `createdAt`         | `DateTime`     | Timestamp when the role was created.            | 8 bytes       | Auto-generated                  | Current timestamp | System      | -                                    | Read (Public) | `"2024-01-10T08:45:00Z"` |

---

###  Sample of Bitwise Representation of Permissions

| **Permission**    | **Bit Position** | **Decimal Value** |
|------------------|---------------|----------------|
| `READ`          | `0`           | `1`           |
| `WRITE`         | `1`           | `2`           |
| `DELETE`        | `2`           | `4`           |
---
