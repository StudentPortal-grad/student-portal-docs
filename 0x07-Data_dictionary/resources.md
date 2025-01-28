### Data Dictionary for `resources` Table

| **Data Element Name** | **Data Type** | **Description**                                                                 | **Length/Size** | **Constraints/Rules** | **Default Value** | **Source** | **Relationships** | **Permissions/Access** | **Examples** |
|----------------------|--------------|-----------------------------------------------------------------------------|---------------|---------------------|-----------------|-----------|---------------|--------------------|------------|
| `id`                | `ObjectId`    | Unique identifier for the resource (primary key).                           | 24 bytes      | Primary key, unique | Auto-generated  | System    | Referenced in `interactions`, `categories`, `users` | Read (Public), Write (Uploader, Admin) | `507f1f77bcf86cd799439100` |
| `title`             | `String`      | Title of the resource.                                                      | 255 chars     | Required            | -               | User input | -             | Read (Public), Write (Uploader, Admin) | `"Introduction to React"` |
| `description`       | `String`      | Brief description of the resource.                                          | 1000 chars    | Optional            | -               | User input | -             | Read (Public), Write (Uploader, Admin) | `"Comprehensive guide to React.js"` |
| `fileUrl`          | `String`      | URL pointing to the uploaded resource file.                                | 2000 chars    | Required            | -               | System     | -             | Read (Public), Write (Uploader) | `"https://cdn.example.com/files/react-guide.pdf"` |
| `tags`              | `Array<String>`| List of tags associated with the resource.                                 | Variable      | Optional            | `[]`            | User input | -             | Read (Public), Write (Uploader, Admin) | `["React", "JavaScript", "Web Development"]` |
| `visibility`        | `String`      | Defines who can see the resource (`public`, `private`, `community`).        | 10 chars      | Enum values only    | `public`        | User input | -             | Read (Public), Write (Uploader, Admin) | `"community"` |
| `communityId`       | `ObjectId`    | ID of the community if `visibility = 'community'`.                          | 24 bytes      | Optional, must exist in `communities.id` | `null`          | User input | References `communities.id` | Read (Community members), Write (Uploader, Admin) | `"507f1f77bcf86cd799439105"` |
| `category`          | `String`      | Category of the resource (e.g., `Engineering`, `Design`, etc.).              | 50 chars      | Enum or category reference | -               | User input | Can be replaced with `categoryId` | Read (Public), Write (Uploader, Admin) | `"Software"` |
| `interactions`      | `JSONB`       | Stores embedded interactions (downloads, ratings, comments).                | Variable      | See `interactions structure` | `{}`            | System     | -             | Read (Public), Write (System) | `{"downloads": 25, "ratings": [{"userId": "507...", "rating": 5}]}` |
| `uploaderId`        | `ObjectId`    | ID of the user who uploaded the resource.                                   | 24 bytes      | Must exist in `users.id` | -               | User input | References `users.id` | Read (Public), Write (System) | `"507f1f77bcf86cd799439102"` |
| `createdAt`         | `DateTime`    | Timestamp when the resource was created.                                    | 8 bytes       | Auto-generated      | Current timestamp | System | -             | Read (Public) | `"2024-01-10T08:45:00Z"` |
| `updatedAt`         | `DateTime`    | Timestamp when the resource was last updated.                               | 8 bytes       | Auto-updated        | Current timestamp | System | -             | Read (Public) | `"2024-01-12T12:30:00Z"` |

---

### Embedded `interactions` Structure

| **Data Element Name** | **Data Type** | **Description** | **Constraints/Rules** | **Examples** |
|----------------------|--------------|----------------|---------------------|--------------|
| `downloads`         | `Number`      | Count of downloads. | Must be non-negative | `25` |
| `ratings`           | `Array<JSON>` | Array of user ratings. | Each entry contains `userId`, `rating`, `createdAt`. | `[{"userId": "507f1f77bcf86cd799439200", "rating": 4, "createdAt": "2024-01-12T10:15:00Z"}]` |
| `comments`          | `Array<JSON>` | Array of comments left by users. | Each entry contains `id`, `userId`, `content`, `createdAt`, and `attachments`. | `[{"id": "507f1f77bcf86cd799439300", "userId": "507f1f77bcf86cd799439201", "content": "Great resource!", "createdAt": "2024-01-12T11:00:00Z"}]` |

---
