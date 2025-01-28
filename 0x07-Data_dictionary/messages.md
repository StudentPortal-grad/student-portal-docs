### Data Dictionary for `messages` Table

| **Data Element Name** | **Data Type** | **Description** | **Length/Size** | **Constraints/Rules** | **Default Value** | **Source** | **Relationships** | **Permissions/Access** | **Examples** |
|----------------------|--------------|----------------|---------------|------------------|---------------|--------|--------------|-----------------|----------|
| `id` | `ObjectId` | Unique identifier for the message (primary key). | 24 bytes | Primary key, unique | Auto-generated | System | Referenced in `users`, `conversations` | Read (Sender, Receiver), Write (Sender) | `"60d21b4667d0d8992e610c85"` |
| `senderId` | `ObjectId` | Reference to the sender user. | 24 bytes | Must exist in `users.id` | - | System | References `users.id` | Read (Sender, Receiver), Write (Sender) | `"60d21b4667d0d8992e610c90"` |
| `content` | `String` | Text content of the message. | Variable | Optional | - | User Input | - | Read (Sender, Receiver), Write (Sender) | `"Hello, how are you?"` |
| `attachments` | `JSONB` | Array of attachment objects. | Variable | Optional | `[]` | User Input | - | Read (Sender, Receiver), Write (Sender) | `[{"type": "file", "resource": "https://example.com/file.pdf"}]` |
| `status` | `String` | Status of the message. | 10 characters | Must be one of: `'sent'`, `'delivered'`, `'read'` | `'sent'` | System | - | Read (Sender, Receiver), Write (System) | `"delivered"` |
| `createdAt` | `DateTime` | Timestamp when the message was sent. | 8 bytes | Auto-generated at creation | Current timestamp | System | - | Read (Sender, Receiver) | `"2024-01-28T12:00:00Z"` |

---

### Embedded `attachments` Structure

| **Data Element Name** | **Data Type** | **Description** | **Constraints/Rules** | **Examples** |
|----------------------|--------------|----------------|---------------------|--------------|
| `type` | `String` | Type of attachment (e.g., `'document'`, `'file'`, `'poll'`, `'thread'`). | Must be one of: `'document'`, `'file'`, `'poll'`, `'thread'` | `"file"` |
| `resource` | `String` | Link to the resource (file or document). | Required for file-based attachments | `"https://example.com/image.jpg"` |
| `thread` | `ObjectId` | Reference to a conversation thread (if applicable). | Must exist in `conversations.id` | `"60d21b4667d0d8992e610c95"` |


