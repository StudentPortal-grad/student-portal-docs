# Student Portal Use Cases Documentation

## Table of Contents
1. [User Management](#1-user-management)
2. [Communication](#2-communication)
3. [Resource Management](#3-resource-management)
4. [Event Management](#4-event-management)

## 1. User Management

### 1.1 Authentication

#### UC-101: Sign Up
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | New User                                                                                      |
| **Trigger**             | User clicks on the "Sign Up" button                                                          |
| **Input**               | Institutional email, password, optional profile details (e.g., name, profile picture)        |
| **Validation Steps**    | 1. Verify email domain matches institutional pattern <br> 2. Ensure password meets security criteria (e.g., minimum length, special characters) |
| **Error Handling**      | 1. Display error if email is invalid or not institutional <br> 2. Show password validation errors in real-time <br> 3. Alert if email is already registered |
| **Output**              | User receives a confirmation email. After verifying, they can log in                        |
| **Post-condition**      | Account is created and active                                                               |
| **Priority**            | High                                                                                         |

#### UC-102: Log In
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Registered User                                                                               |
| **Trigger**             | User clicks "Log In" and enters credentials                                                  |
| **Input**               | Email, password                                               |
| **Validation Steps**    | 1. Match email and password to stored credentials       |
| **Error Handling**      | 1. Show "Invalid credentials" for incorrect input <br> 2. Account lock after multiple failed attempts |
| **Output**              | User gains access to the dashboard or main portal                                            |
| **Post-condition**      | User is logged into their profile                                                           |
| **Priority**            | High                                                                                         |

#### UC-103: Password Recovery
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User who forgot their password                                                                |
| **Trigger**             | User clicks "Forgot Password" link                                                           |
| **Input**               | Registered email address                                                                     |
| **Validation Steps**    | 1. Verify email exists in the database <br> 2. Ensure reset link is unique and time-limited  |
| **Error Handling**      | 1. Display "Email not found" for unregistered addresses <br> 2. Expire old reset links      |
| **Output**              | User receives an email with a reset link, sets a new password, and logs in                   |
| **Post-condition**      | Password is updated successfully                                                            |
| **Priority**            | Medium                                                                                       |

### 1.2 Profile Management

#### UC-111: Create Profile
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | New User                                                                                      |
| **Trigger**             | User logs in for the first time and navigates to the "Profile" section                        |
| **Input**               | Profile picture, bio, academic interests, optional details like name and contact information  |
| **Validation Steps**    | 1. Ensure required fields (e.g., bio, academic interests) are filled <br> 2. Validate file type for profile picture upload |
| **Error Handling**      | 1. Display error messages for invalid file types or empty required fields <br> 2. Allow user to retry with correct inputs |
| **Output**              | Profile is saved and viewable by others                                                       |
| **Post-condition**      | Profile setup is complete                                                                    |
| **Priority**            | Medium                                                                                       |

#### UC-112: Update Profile
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Registered User                                                                               |
| **Trigger**             | User navigates to the "Profile" section and clicks "Edit Profile"                             |
| **Input**               | Updated profile picture, bio, academic interests, or other optional details                   |
| **Validation Steps**    | 1. Ensure uploaded files (if any) meet size and format criteria <br> 2. Validate changes to mandatory fields |
| **Error Handling**      | 1. Show real-time validation errors for invalid inputs <br> 2. Allow user to cancel or retry updates |
| **Output**              | Profile updates are saved and reflected on the user's profile page                            |
| **Post-condition**      | Profile reflects the latest changes                                                          |
| **Priority**            | Medium                                                                                       |

## 2. Communication

### 2.1 Messaging

#### UC-201: Direct Messaging
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User searches for a peer or faculty member and opens a chat window                            |
| **Input**               | Text message or attachment (optional)                                                        |
| **Validation Steps**    | 1. Ensure recipient exists in the system <br> 2. Validate message length and attachment size |
| **Error Handling**      | 1. Show error if the recipient is not found <br> 2. Notify if attachment size exceeds limits |
| **Output**              | Message is sent and visible to the recipient                                                 |
| **Post-condition**      | Communication thread is updated for both sender and recipient                                |
| **Priority**            | High                                                                                         |

#### UC-202: Group Chats
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User selects or creates a group chat                                                         |
| **Input**               | Group name, description (for new group), and messages from members                           |
| **Validation Steps**    | 1. Validate uniqueness of group name <br> 2. Ensure members exist in the system             |
| **Error Handling**      | 1. Notify if group creation fails due to name conflict <br> 2. Alert if a message delivery fails |
| **Output**              | Messages are exchanged and visible to group members                                          |
| **Post-condition**      | Group chat is active and accessible to members                                               |
| **Priority**            | Medium                                                                                       |

### 2.2 Groups and Communities

#### UC-211: Create Groups
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User, Faculty, or Admin                                                                       |
| **Trigger**             | Actor clicks on "Create Group"                                                               |
| **Input**               | - Group name <br> - Description <br> - Group type (Official/Community) <br> - Optional group image |
| **Validation Steps**    | 1. Ensure group name is unique <br> 2. Validate description length and file type for images <br> 3. **For Official Groups:** <br> - Verify creator has Admin/Faculty permissions <br> - Validate academic purpose <br> **For Community Groups:** <br> - Standard validation only |
| **Error Handling**      | 1. Show error if group name already exists <br> 2. Notify if file upload fails <br> 3. Display permission error for unauthorized official group creation |
| **Output**              | Group is created and added to appropriate directory: <br> - Official Groups directory for faculty/admin created groups <br> - Community Groups directory for user-created groups |
| **Post-condition**      | - Official groups: Only modifiable by faculty/admin <br> - Community groups: Modifiable by creator |
| **Priority**            | High                                                                                         |

#### UC-212: Join Groups
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User browses group directories (Official or Community) and clicks "Join"                    |
| **Input**               | Selected group                                                                               |
| **Validation Steps**    | 1. Verify group access settings: <br> - Official Groups: Open or Invite-only <br> - Community Groups: Public or private |
| **Error Handling**      | 1. Display "Access Denied" for invite-only/private groups <br> 2. Notify if the group is at member capacity |
| **Output**              | User is added as a member of the group                                                       |
| **Post-condition**      | User receives updates and access to group discussions                                        |
| **Priority**            | Medium                                                                                       |

#### UC-213: Manage Groups
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Group Owner (Faculty/Admin for Official Groups, Creator for Community Groups)                  |
| **Trigger**             | Actor navigates to group and selects "Manage Group"                                           |
| **Input**               | - Updated group details (name, description, image) <br> - Member management actions (add/remove) <br> - Group settings changes (privacy, permissions) |
| **Validation Steps**    | 1. Validate actor's permissions: <br> - For Official Groups: Must be Faculty/Admin <br> - For Community Groups: Must be group creator <br> 2. Verify member operations are valid <br> 3. Ensure updates meet platform guidelines |
| **Error Handling**      | 1. Show error if actor lacks required permissions <br> 2. Display error for invalid member operations <br> 3. Notify if updates fail to save <br> 4. Alert if settings changes violate platform rules |
| **Output**              | Group settings, membership, and details are updated according to actor's permissions           |
| **Post-condition**      | - Official Groups: Changes reflected with institutional guidelines maintained <br> - Community Groups: Changes reflected within platform guidelines |
| **Priority**            | High                                                                                          |                                         |

#### UC-214: Start a Discussion in a Group
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Group Member                                                                                 |
| **Trigger**             | User clicks "Start a Discussion" within a group                                              |
| **Input**               | Title, body content, optional attachments or media                                           |
| **Validation Steps**    | 1. Ensure title is not empty <br> 2. Validate content length <br> 3. Check file type and size of attachments |
| **Error Handling**      | 1. Show error if title or content is invalid <br> 2. Notify if attachment upload fails       |
| **Output**              | Discussion is created and visible to all group members                                       |
| **Post-condition**      | Other group members can view, reply to, or interact with the discussion                      |
| **Priority**            | High                                                                                         |

#### UC-215: Reply to a Discussion
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Group Member                                                                                 |
| **Trigger**             | User clicks "Reply" on an existing discussion                                                |
| **Input**               | Reply content, optional attachments                                                          |
| **Validation Steps**    | 1. Ensure reply is not empty <br> 2. Validate file types and sizes for attachments           |
| **Error Handling**      | 1. Show error for invalid inputs <br> 2. Notify if attachment upload fails                   |
| **Output**              | Reply is added to the discussion thread                                                      |
| **Post-condition**      | Other members see the reply in real-time or when they refresh                                |
| **Priority**            | Medium                                                                                       |

#### UC-216: Pin/Highlight a Discussion
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Admin, Faculty, or Group Moderator                                                            |
| **Trigger**             | Moderator selects "Pin" or "Highlight" on a discussion                                       |
| **Input**               | Selected discussion                                                                          |
| **Validation Steps**    | 1. Ensure the actor has appropriate permissions                                              |
| **Error Handling**      | Display error if permissions are invalid                                                     |
| **Output**              | Discussion is marked as pinned or highlighted, appearing at the top of the discussion list   |
| **Post-condition**      | Group members easily find the pinned/highlighted discussion                                  |
| **Priority**            | Medium                                                                                       |

## 3. Resource Management

### 3.1 Academic Resources

#### UC-301: Upload Academic Materials
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User clicks "Upload Resource"                                                                |
| **Input**               | File (e.g., PDF, DOCX), title, description, and tags                                         |
| **Validation Steps**    | 1. Check file type and size <br> 2. Ensure title and description are not empty              |
| **Error Handling**      | 1. Show error for unsupported file types or size limit exceeded <br> 2. Notify if upload fails |
| **Output**              | Resource is uploaded and visible in the shared resources directory                           |
| **Post-condition**      | Other users can view, download, or interact with the resource                                |
| **Priority**            | High                                                                                         |

#### UC-302: Interact with Resources
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User selects a resource to comment on, rate, or download                                     |
| **Input**               | Comment, rating (stars), or download action                                                  |
| **Validation Steps**    | 1. Validate rating scale (e.g., 1-5 stars) <br> 2. Ensure comments are not empty             |
| **Error Handling**      | Notify if the interaction fails to save                                                      |
| **Output**              | Interaction (comment or rating) is recorded and visible to others                            |
| **Post-condition**      | Resource interaction enhances engagement and feedback                                        |
| **Priority**            | Medium                                                                                       |

## 4. Event Management

### 4.1 Event Operations

#### UC-401: Create Events
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | Faculty, Admin                                                                                 |
| **Trigger**             | Faculty/Admin clicks "Create Event"                                                          |
| **Input**               | Event name, date, time, location, description, and optional image                            |
| **Validation Steps**    | 1. Check date and time validity (e.g., no past dates) <br> 2. Ensure required fields are filled |
| **Error Handling**      | 1. Show error if date or time is invalid <br> 2. Notify if image upload fails                |
| **Output**              | Event is created and visible in the event directory                                          |
| **Post-condition**      | Users can view and RSVP to the event                                                         |
| **Priority**            | High                                                                                         |

#### UC-402: RSVP to Events
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User clicks "RSVP" on an event                                                               |
| **Input**               | Event selection                                                                              |
| **Validation Steps**    | Ensure event is not full (if capacity is set)                                                |
| **Error Handling**      | Notify if RSVP fails or if event is full                                                     |
| **Output**              | User's RSVP is recorded and confirmed                                                       |
| **Post-condition**      | User receives event updates and reminders (if applicable)                                    |
| **Priority**            | Medium                                                                                       |

#### UC-403: Sync Events to Calendar
| **Field**               | **Details**                                                                                     |
|-------------------------|------------------------------------------------------------------------------------------------|
| **Actor**               | User                                                                                          |
| **Trigger**             | User clicks "Sync to Calendar" for an event                                                  |
| **Input**               | Calendar application integration (Google Calendar, Outlook, etc.)                           |
| **Validation Steps**    | Ensure user grants necessary permissions for calendar sync                                   |
| **Error Handling**      | Notify if sync fails due to connectivity or permission issues                                |
| **Output**              | Event is added to the user's calendar                                                        |
| **Post-condition**      | User sees the event in their personal calendar                                               |
| **Priority**            | Low                                                                                          |

