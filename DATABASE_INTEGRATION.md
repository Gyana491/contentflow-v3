# Database Integration for Post Publishing

This document outlines the database integration implemented to ensure that LinkedIn posts are properly saved to the database when published or scheduled.

## Overview

The system now saves all posts to the database in the following scenarios:
1. **Content Generation**: When content is generated, it's saved as a draft
2. **Post Publishing**: When posts are published to LinkedIn, they're saved as published
3. **Post Scheduling**: When posts are scheduled, they're saved as scheduled

## Database Schema

The system uses the following tables for post management:

### Posts Table
- `id`: Unique identifier
- `userId`: User who created the post
- `workflowRunId`: Optional link to workflow run
- `title`: Post title
- `content`: Post content
- `hashtags`: Array of hashtags
- `contentType`: Type of content (ARTICLE, TREND, NEWS, TUTORIAL)
- `tone`: Tone of content (PROFESSIONAL, CASUAL, INSPIRING, INFORMATIVE)
- `status`: Post status (DRAFT, PUBLISHED, SCHEDULED, FAILED)
- `isPublished`: Boolean indicating if published to LinkedIn
- `publishedAt`: When the post was published
- `linkedInPostId`: LinkedIn's post ID
- `linkedInUrl`: URL to the LinkedIn post

### Scheduled Posts Table
- `id`: Unique identifier
- `userId`: User who scheduled the post
- `postId`: Reference to the post
- `scheduledAt`: When the post is scheduled to be published
- `timezone`: User's timezone
- `status`: Schedule status (PENDING, PUBLISHED, FAILED, CANCELLED)

## API Endpoints

### Content Generation
- **POST** `/generate` - Generates content and saves as draft
  - Requires authentication
  - Saves post to database with status `DRAFT`

### Post Publishing
- **POST** `/linkedin/publish` - Publishes text-only post
  - Saves post to database with status `PUBLISHED`
  - Updates `linkedInPostId` and `linkedInUrl`

- **POST** `/linkedin/publish-with-image` - Publishes post with image
  - Saves post to database with status `PUBLISHED`
  - Handles image upload to LinkedIn
  - Updates `linkedInPostId` and `linkedInUrl`

### Post Scheduling
- **POST** `/linkedin/schedule` - Schedules post for later publication
  - Saves post to database with status `SCHEDULED`
  - Creates entry in `ScheduledPost` table

### Post Retrieval
- **GET** `/linkedin/user-posts` - Retrieves user's posts from database
  - Returns all posts for the authenticated user
  - Includes scheduled post information

## Frontend Integration

### Content Generation Form
- Updated to include authentication headers
- Saves generated content as draft in database
- Includes metadata (contentType, tone, hashtags) when publishing

### Publishing Flow
1. User generates content → Saved as draft
2. User publishes content → Updated to published status
3. User schedules content → Saved as scheduled with schedule details

### Posts List Component
- Displays all user's posts from database
- Shows post status, creation date, and publication date
- Provides links to published LinkedIn posts
- Displays hashtags and content type

## Authentication

All database operations require user authentication:
- Content generation requires valid JWT token
- Post publishing requires LinkedIn authentication
- Post retrieval requires LinkedIn authentication

## Error Handling

The system includes comprehensive error handling:
- Database connection errors
- LinkedIn API errors
- Authentication errors
- Validation errors

## Benefits

1. **Data Persistence**: All posts are saved to database
2. **Post History**: Users can view all their posts
3. **Scheduling**: Posts can be scheduled for future publication
4. **Analytics**: Post data can be used for analytics
5. **Backup**: Posts are backed up in database
6. **Audit Trail**: Complete history of post creation and publication

## Usage

1. **Generate Content**: Content is automatically saved as draft
2. **Publish Immediately**: Post is published to LinkedIn and saved as published
3. **Schedule Post**: Post is saved as scheduled with schedule details
4. **View Posts**: All posts are displayed in the posts list component

## Future Enhancements

1. **Post Analytics**: Track engagement metrics
2. **Post Editing**: Edit published posts
3. **Bulk Operations**: Schedule multiple posts
4. **Post Templates**: Save and reuse post templates
5. **Export Data**: Export post data for analysis 