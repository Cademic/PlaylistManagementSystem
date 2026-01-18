# Milestone 1 – Project Proposal and Design Document


- **Course:** CST-391 Web Application Development
- **Instructor** Professor James Sparks
- **Author:** Carter Wright
- **Date:** January 18, 2026

## Feature Proposal

The proposed feature for the music application is a **Playlist Management system**. This feature allows customers to create, manage, and organize playlists made up of songs in the application. Playlists enhance the user experience by giving customers a personalized way to group and revisit their favorite music.

Role-Based Access Control (RBAC) will differentiate how customers and admins interact with this feature. Customers can create and manage their own playlists, while admins can view all playlists across the system and remove inappropriate or duplicate content. This separation of privileges ensures proper moderation while maintaining user freedom.

----

## User Stories

- **As a customer**, I want to create playlists so that I can organize my favorite songs.
- **As a customer**, I want to add or remove songs from my playlists so that I can customize my listening experience.
- **As an admin**, I want to view all user-created playlists so that I can monitor and moderate content when necessary.
- **As an admin**, I want to delete playlists that violate content rules so that the platform remains appropriate for all users.

----

## Data Model and Design

To support playlists, the following data entities are required:

![Music player UML diagram](../Images/Diagrams/musicplayerUML.png)

### Playlist
- id (primary key)
- name
- userId (foreign key referencing User)
- createdAt

### PlaylistSong (junction table)
- playlistId (foreign key)
- songId (foreign key)

### Relationships
- One user can have many playlists
- One playlist can contain many songs
- Songs can belong to multiple playlists

This design supports efficient querying and enforces ownership of playlists by users.

----

## API Design

The following REST API endpoints are required:

### Customer Endpoints
- **POST /api/playlists**  
  Creates a new playlist (authenticated customer)

- **GET /api/playlists**  
  Returns playlists owned by the logged-in customer

- **POST /api/playlists/{id}/songs**  
  Adds a song to a playlist (playlist owner only)

- **DELETE /api/playlists/{id}/songs/{songId}**  
  Removes a song from a playlist (playlist owner only)

### Admin Endpoints
- **GET /api/admin/playlists**  
  Returns all playlists in the system (admin only)

- **DELETE /api/admin/playlists/{id}**  
  Deletes any playlist (admin only)

All endpoints require authentication. Admin routes are restricted by role.

----

## UI and UX Design

### Customer Pages
- **/playlists**  
  Displays the customer’s playlists
- **/playlists/create**  
  Allows customers to create a new playlist
- **/playlists/{id}**  
  Manage songs within a playlist

### Admin Pages
- **/admin/playlists**  
  Displays all playlists across the platform with moderation options

Wireframes will show a simple list-based UI for playlists and a management table for admins.

----

## Security and Route Protection

RBAC will be enforced using role checks within Next.js middleware and protected API routes.

- Customers must be authenticated to access playlist pages
- Customers can only modify their own playlists
- Admin-only routes require the `admin` role
- Only admins can delete playlists created by other users

This role-based approach simplifies permission management by assigning privileges to roles rather than individual users.

----

## Assumptions and Constraints

- Authentication and role information are already implemented based on course tutorials
- Only two roles exist: admin and consumer
- Playlist sharing is not included in this milestone
- Performance optimizations are deferred until later milestones

----

## References

- Course tutorials and lecture materials  
- ChatGPT (2026/01/15). Prompt: “Design a markdown doc I can use for a project proposal.”  
- Role-Based Access Control concepts referenced from NIST documentation
