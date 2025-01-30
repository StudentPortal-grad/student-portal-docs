### Data Dictionary for `discussions` Table

| **Data Element Name** | **Data Type**  | **Description**                                     | **Length/Size** | **Constraints/Rules**            | **Default Value** | **Source**  | **Relationships**                        | **Permissions/Access** | **Examples** |
|----------------------|---------------|----------------------------------------------------|---------------|--------------------------------|-----------------|------------|--------------------------------|--------------------|------------|
| `id`                | `ObjectId`     | Unique identifier for the discussion (primary key). | 24 bytes      | Primary key, unique, auto-generated | Auto-generated  | System     | Referenced in `replies` and `votes`    | Read (Public/Community), Write (Creator) | `"507f1f77bcf86cd799439200"` |
| `communityId`       | `ObjectId`     | ID of the community the discussion belongs to.     | 24 bytes      | Foreign key, references `communities.id` | Required        | System     | References `communities.id`            | Read (Public/Community), Write (System) | `"507f1f77bcf86cd799439100"` |
| `title`             | `String`       | Title of the discussion.                           | 255 chars     | Required                        | Required        | User input  | -                                    | Read (Public/Community), Write (Creator) | `"Best Practices for Web Development"` |
| `content`           | `String`       | Main content/body of the discussion.              | Variable      | Required                        | Required        | User input  | -                                    | Read (Public/Community), Write (Creator) | `"What are the best practices for web development?"` |
| `creator`           | `ObjectId`     | ID of the user who created the discussion.        | 24 bytes      | Foreign key, references `users.id` | Required        | User input  | References `users.id`                  | Read (Public/Community), Write (Creator) | `"507f1f77bcf86cd799439101"` |
| `attachments`       | `JSONB`        | Array of attachment objects.                      | Variable      | Optional                        | `[]`            | User input  | See "Attachment Structure" below      | Read (Public/Community), Write (Creator) | `[{"type": "file", "resource": "https://files.com/doc.pdf"}]` |
| `replies`           | `JSONB`        | Embedded array of reply objects.                  | Variable      | Optional                        | `[]`            | User input  | See "Reply Structure" below           | Read (Public/Community), Write (Participants) | `[{"id": "507f1f77bcf86cd799439300", "content": "I agree!", "creator": "507f1f77bcf86cd799439102"}]` |
| `votes`             | `JSONB`        | Embedded array of vote objects.                   | Variable      | Optional                        | `[]`            | User input  | See "Vote Structure" below            | Read (Public/Community), Write (Participants) | `[{"userId": "507f1f77bcf86cd799439103", "voteType": "upvote"}]` |
| `status`            | `String`       | Status of the discussion (`open`, `closed`, `archived`). | 10 chars      | Enum values only               | `open`          | System      | -                                    | Read (Public/Community), Write (System) | `"closed"` |
| `createdAt`         | `DateTime`     | Timestamp when the discussion was created.        | 8 bytes       | Auto-generated                  | Current timestamp | System      | -                                    | Read (Public/Community) | `"2024-01-10T08:45:00Z"` |
| `updatedAt`         | `DateTime`     | Timestamp when the discussion was last updated.   | 8 bytes       | Auto-updated                    | Current timestamp | System      | -                                    | Read (Public/Community) | `"2024-01-12T12:30:00Z"` |

---

### Embedded `attachments` Structure

| **Data Element Name** | **Data Type** | **Description** | **Constraints/Rules** | **Examples** |
|----------------------|--------------|----------------|---------------------|--------------|
| `type`             | `String`      | Type of attachment (`document`, `file`, `poll`, etc.). | Enum values only | `"file"` |
| `resource`         | `String`      | URL to the resource or file. | Must be a valid URL | `"https://files.com/doc.pdf"` |

---

### Embedded `replies` Structure

| **Data Element Name** | **Data Type** | **Description** | **Constraints/Rules** | **Examples** |
|----------------------|--------------|----------------|---------------------|--------------|
| `id`               | `ObjectId`    | Unique identifier for the reply. | Primary key, unique | `"507f1f77bcf86cd799439300"` |
| `content`          | `String`      | Content of the reply. | Required | `"I agree!"` |
| `creator`          | `ObjectId`    | User ID of the reply author. | Foreign key, references `users.id` | `"507f1f77bcf86cd799439102"` |
| `createdAt`        | `DateTime`    | Timestamp when the reply was created. | Auto-generated | `"2024-01-11T09:00:00Z"` |
| `attachments`      | `Array<JSON>` | Optional attachments related to the reply. | See "Attachment Structure" | `[{"type": "file", "resource": "https://files.com/image.png"}]` |

---

### Embedded `votes` Structure

| **Data Element Name** | **Data Type** | **Description** | **Constraints/Rules** | **Examples** |
|----------------------|--------------|----------------|---------------------|--------------|
| `userId`           | `ObjectId`    | ID of the user who voted. | Foreign key, references `users.id` | `"507f1f77bcf86cd799439103"` |
| `voteType`         | `String`      | Type of vote (`upvote`, `downvote`). | Enum values only | `"upvote"` |
| `createdAt`        | `DateTime`    | Timestamp when the vote was cast. | Auto-generated | `"2024-01-11T09:15:00Z"` |

---
