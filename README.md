# ContentFlow v3 - AI-Powered Viral LinkedIn Content creation & Scheduling tool to grow your reach & engagement

A comprehensive platform for generating, managing, and publishing viral LinkedIn content using AI-powered workflows. ContentFlow combines advanced AI content generation with seamless LinkedIn integration, offering a complete solution for professional content creators and businesses.

![1754401277789](images/README/1754401277789.png)

## 🚀 Features

### 🤖 AI-Powered Content Generation

- **Advanced AI Workflows**: Uses Mastra workflows for intelligent content generation
- **Multiple Content Types**: Articles, trends, news, and tutorials
- **Tone Customization**: Professional, casual, inspiring, and informative tones
- **Smart Hashtag Generation**: Automatically generates relevant hashtags for better reach
- **Real-time Generation**: Fast content generation with loading states

### 📱 LinkedIn Integration

- **OAuth Authentication**: Secure LinkedIn account connection
- **Direct Publishing**: Publish posts directly to LinkedIn
- **Image Support**: Upload and attach images to posts
- **Post Scheduling**: Schedule posts for future publication
- **Post Management**: View and manage all published posts

### 📊 Content Management

- **Draft System**: Save and edit content before publishing
- **Post History**: Complete history of all generated and published posts
- **Scheduling Calendar**: Visual calendar for post scheduling
- **Analytics Tracking**: Monitor post performance and engagement
- **Bulk Operations**: Manage multiple posts efficiently

### 🔐 User Management

- **Secure Authentication**: JWT-based authentication system
- **User Profiles**: Complete user profile management
- **Settings & Preferences**: Customizable posting preferences
- **Timezone Support**: Global timezone handling for scheduling

## 🏗️ Architecture

### System Overview

![1754401121831](images/README/1754401121831.png)

ContentFlow v3 is built as a full-stack application with a microservices architecture:

```


┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Frontend      │    │   Backend       │    │   Database      │
│   (Next.js)     │◄──►│   (Hono/Bun)    │◄──►│   (PostgreSQL)  │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   LinkedIn      │    │   Mastra AI     │    │   Cron Jobs     │
│   API           │    │   Workflows     │    │   (Scheduler)   │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### Frontend Architecture (Next.js 15)

- **Framework**: Next.js 15 with App Router
- **Language**: TypeScript
- **Styling**: Tailwind CSS v4 with shadcn/ui components
- **State Management**: Zustand for global state
- **Authentication**: JWT-based with secure token storage
- **UI Components**: Radix UI primitives with custom styling

### Backend Architecture (Hono + Bun)

- **Runtime**: Bun for high-performance JavaScript runtime
- **Framework**: Hono for lightweight, fast web framework
- **Database**: Prisma ORM with PostgreSQL
- **Authentication**: JWT with bcrypt for password hashing
- **API Design**: RESTful API with proper error handling
- **Cron Jobs**: Automated post scheduling and publishing

### Database Schema

The application uses a comprehensive PostgreSQL schema with the following main entities:

#### Core Models

- **User**: User accounts and authentication
- **LinkedInAuth**: LinkedIn OAuth integration
- **Post**: Content posts with metadata
- **ScheduledPost**: Post scheduling management
- **WorkflowRun**: AI workflow execution tracking
- **UserSettings**: User preferences and settings

#### Key Relationships

- One-to-one: User ↔ LinkedInAuth, User ↔ UserSettings
- One-to-many: User → Posts, User → WorkflowRuns
- One-to-one: Post ↔ ScheduledPost

## 🛠️ Tech Stack

### Frontend

- **Framework**: Next.js 15.4.5
- **Language**: TypeScript 5
- **UI Library**: React 19.1.0
- **Styling**: Tailwind CSS v4
- **Components**: shadcn/ui + Radix UI
- **State Management**: Zustand 4.5.0
- **Forms**: React Hook Form + Zod validation
- **Icons**: Lucide React
- **Themes**: next-themes for dark/light mode

### Backend

- **Runtime**: Bun
- **Framework**: Hono 4.8.12
- **Language**: TypeScript
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: JWT + bcryptjs
- **CORS**: Cross-origin resource sharing
- **Scheduling**: Croner for cron jobs
- **Validation**: Zod schema validation

### External Services

- **AI Workflows**: Mastra client-js SDK with custom agents and workflows
- **LinkedIn API**: Official LinkedIn API v2
- **Content Generation**: OpenAI integration via AI SDK
- **Research Tool**: Perplexity AI for real-time web research

## 📁 Project Structure

```
contentflow-v3/
├── frontend/                    # Next.js frontend application
│   ├── src/
│   │   ├── app/                # Next.js App Router pages
│   │   │   ├── api/           # API routes
│   │   │   ├── auth/          # Authentication pages
│   │   │   ├── dashboard/     # Main dashboard
│   │   │   │   ├── create/    # Content creation
│   │   │   │   ├── posts/     # Post management
│   │   │   │   ├── scheduled/ # Scheduled posts
│   │   │   │   ├── calendar/  # Calendar view
│   │   │   │   └── settings/  # User settings
│   │   │   └── layout.tsx     # Root layout
│   │   ├── components/        # Reusable UI components
│   │   ├── hooks/            # Custom React hooks
│   │   ├── lib/              # Utilities and services
│   │   └── services/         # API service layer
│   ├── public/               # Static assets
│   └── package.json
├── server/                    # Hono backend application
│   ├── src/
│   │   ├── routes/           # API route handlers
│   │   ├── services/         # Business logic services
│   │   ├── middleware/       # Custom middleware
│   │   ├── utils/           # Utility functions
│   │   └── lib/             # External service integrations
│   ├── prisma/              # Database schema and migrations
│   └── package.json
├── mastra/                   # Mastra AI workflow configurations
│   ├── src/mastra/
│   │   ├── agents/          # AI agents for content generation
│   │   │   ├── content-agent.ts    # Main content creation agent
│   │   │   └── research-agent.ts   # Research and data gathering agent
│   │   ├── workflows/       # AI workflow definitions
│   │   │   └── content-workflow.ts # Content generation workflow
│   │   ├── tools/           # AI tools and integrations
│   │   │   └── perplexity-tool.ts  # Perplexity AI research tool
│   │   └── index.ts         # Mastra configuration and exports
│   ├── package.json         # Mastra dependencies
│   └── README.md           # Mastra setup instructions
└── README.md                # This file
```

## 🚀 Getting Started

### Prerequisites

- **Node.js**: 18+ (for frontend)
- **Bun**: Latest version (for backend)
- **PostgreSQL**: 14+ with connection details
- **LinkedIn Developer Account**: For API access
- **Mastra Server**: Running on localhost:4111
- **OpenAI API Key**: For AI content generation
- **Perplexity API Key**: For real-time research (optional)

### Environment Setup

#### Frontend (.env)

```env
NEXT_PUBLIC_API_URL=http://localhost:8080
NEXT_PUBLIC_APP_URL=http://localhost:3000
```

#### Backend (.env)

```env
# Database
DATABASE_URL="postgresql://username:password@localhost:5432/contentflow"
DIRECT_URL="postgresql://username:password@localhost:5432/contentflow"

# JWT
JWT_SECRET=your-super-secret-jwt-key

# LinkedIn OAuth
LINKEDIN_CLIENT_ID=your-linkedin-client-id
LINKEDIN_CLIENT_SECRET=your-linkedin-client-secret
LINKEDIN_REDIRECT_URI=http://localhost:8080/api/auth/linkedin/callback

# Mastra
MASTRA_API_URL=http://localhost:4111
MASTRA_API_KEY=your-mastra-api-key

# AI Services
OPENAI_API_KEY=your-openai-api-key
PERPLEXITY_API_KEY=your-perplexity-api-key

# Server
PORT=8080
NODE_ENV=development
```

### Installation

1. **Clone the repository**

```bash
git clone <repository-url>
cd contentflow-v3
```

2. **Install frontend dependencies**

```bash
cd frontend
npm install
```

3. **Install backend dependencies**

```bash
cd ../server
bun install
```

4. **Setup Mastra AI workflows**

```bash
cd ../mastra
npm install
```

5. **Setup database**

```bash
# Generate Prisma client
bun run db:generate

# Run migrations
bun run db:migrate

# Push schema (for development)
bun run db:push
```

6. **Start the development servers**

Terminal 1 (Mastra AI Server):

```bash
cd mastra
npm run dev
```

Terminal 2 (Backend):

```bash
cd server
bun run dev
```

Terminal 3 (Frontend):

```bash
cd frontend
npm run dev
```

7. **Access the application**

- Frontend: http://localhost:3000
- Backend API: http://localhost:8080
- Mastra AI Server: http://localhost:4111
- Prisma Studio: http://localhost:5555 (run `bun run db:studio`)

## 🤖 Mastra AI Workflows

### AI Architecture Overview

ContentFlow v3 uses a sophisticated AI workflow system built with Mastra framework, consisting of specialized agents and tools for intelligent content generation:

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Research      │    │   Content       │    │   Perplexity    │
│   Agent         │◄──►│   Agent         │◄──►│   AI Tool       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Topic         │    │   Content       │    │   Real-time     │
│   Research      │    │   Generation    │    │   Web Data      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

### AI Agents

#### Research Agent

- **Purpose**: Gathers comprehensive information on any given topic
- **Model**: Google Gemini 1.5 Pro
- **Tools**: Perplexity AI research tool
- **Responsibilities**:
  - Real-time web research using Perplexity AI
  - Trend analysis and actionable insights
  - Key statistics and data point identification
  - Industry expert opinion gathering
  - Content angle identification for social media

#### Content Agent

- **Purpose**: Generates viral LinkedIn content from research data
- **Model**: OpenAI GPT-4 (via AI SDK)
- **Capabilities**:
  - Creates engaging LinkedIn posts with hooks
  - Generates relevant hashtags
  - Optimizes content for LinkedIn engagement
  - Adapts tone (professional, casual, inspiring, informative)
  - Includes call-to-action elements

### AI Workflows

#### Content Generation Workflow

The main workflow orchestrates the entire content creation process:

1. **Research Step** (`research-topic`)

   - Input: Topic, content type, tone, scheduling info
   - Process: Uses Research Agent to gather comprehensive data
   - Output: Research data, sources, key insights
2. **Content Generation Step** (`generate-content`)

   - Input: Research data from previous step
   - Process: Uses Content Agent to create viral LinkedIn post
   - Output: Complete LinkedIn post with hashtags

### AI Tools

#### Perplexity Research Tool

- **Purpose**: Real-time web research and data gathering
- **API**: Perplexity AI API (with fallback to mock data)
- **Features**:
  - Real-time web search and research
  - Source citation and verification
  - Key insight extraction
  - Trend identification
  - Fallback mechanism for API failures

### Workflow Configuration

The workflow is configured with the following schema:

```typescript
// Input Schema
{
  topic: string,                    // Topic to research
  contentType: 'article' | 'trend' | 'news' | 'tutorial',
  tone: 'professional' | 'casual' | 'inspiring' | 'informative',
  scheduledTime?: string           // Optional scheduling
}

// Output Schema
{
  linkedinPost: string,            // Generated post content
  hashtags: string[],              // Relevant hashtags
  topic: string                    // Original topic
}
```

### Environment Variables for AI

#### Mastra Server (.env)

```env
OPENAI_API_KEY=your-openai-api-key
PERPLEXITY_API_KEY=your-perplexity-api-key
```

### AI Development

#### Adding New Agents

1. Create agent file in `mastra/src/mastra/agents/`
2. Define agent with model and tools
3. Export from `mastra/src/mastra/index.ts`

#### Adding New Tools

1. Create tool file in `mastra/src/mastra/tools/`
2. Define tool with input/output schemas
3. Add to agent's tools configuration

#### Modifying Workflows

1. Edit workflow in `mastra/src/mastra/workflows/`
2. Define steps with input/output schemas
3. Chain steps using `.then()` method

## 📚 API Documentation

### Authentication Endpoints

- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login
- `POST /api/auth/logout` - User logout
- `GET /api/auth/me` - Get current user

### LinkedIn Integration

- `GET /api/auth/linkedin` - LinkedIn OAuth initiation
- `GET /api/auth/linkedin/callback` - OAuth callback
- `POST /api/linkedin/publish` - Publish text post
- `POST /api/linkedin/publish-with-image` - Publish post with image
- `POST /api/linkedin/schedule` - Schedule post
- `GET /api/linkedin/user-posts` - Get user's posts

### Content Generation

- `POST /api/generate` - Generate AI content
- `GET /api/fetch-content` - Fetch generated content
- `GET /api/status/:runId` - Check workflow status

### Post Management

- `GET /api/posts` - Get user's posts
- `GET /api/posts/:id` - Get specific post
- `PUT /api/posts/:id` - Update post
- `DELETE /api/posts/:id` - Delete post

## 🔧 Development

### Database Commands

```bash
# Generate Prisma client
bun run db:generate

# Create new migration
bun run db:migrate

# Push schema changes
bun run db:push

# Reset database
bun run db:reset

# Open Prisma Studio
bun run db:studio

# Deploy migrations (production)
bun run db:deploy
```

### Frontend Development

```bash
# Start development server
npm run dev

# Build for production
npm run build

# Start production server
npm run start

# Run linting
npm run lint
```

### Backend Development

```bash
# Start development server with hot reload
bun run dev

# Start production server
bun run start
```

### Mastra AI Development

```bash
# Start Mastra development server
cd mastra
npm run dev

# Build Mastra for production
npm run build

# Test Mastra workflows
npm test
```

## 🧪 Testing

### Frontend Testing

```bash
# Run tests
npm test

# Run tests in watch mode
npm test -- --watch
```

### Backend Testing

```bash
# Run tests
bun test

# Run tests with coverage
bun test --coverage
```

## 🚀 Deployment

### Frontend Deployment (Vercel)

1. Connect repository to Vercel
2. Set environment variables
3. Deploy automatically on push

### Backend Deployment

1. **Docker Deployment**

```dockerfile
FROM oven/bun:latest
WORKDIR /app
COPY package.json .
RUN bun install
COPY . .
EXPOSE 8080
CMD ["bun", "run", "start"]
```

2. **Environment Variables**

- Set all required environment variables
- Configure database connection
- Set up LinkedIn OAuth credentials

3. **Database Migration**

```bash
bun run db:deploy
```

## 🔒 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: bcrypt for password security
- **CORS Protection**: Configured CORS policies
- **Input Validation**: Zod schema validation
- **Rate Limiting**: API rate limiting (configurable)
- **HTTPS**: Secure communication in production

## 📊 Monitoring & Analytics

- **Error Tracking**: Comprehensive error handling
- **Performance Monitoring**: Request/response timing
- **Database Monitoring**: Query performance tracking
- **User Analytics**: Post engagement tracking
- **API Usage**: Request volume monitoring

### Development Guidelines

- Follow TypeScript best practices
- Use conventional commit messages
- Add tests for new features
- Update documentation as needed
- Follow the existing code style

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

- **Documentation**: Check the `/docs` folder for detailed guides
- **Issues**: Report bugs via GitHub Issues
- **Discussions**: Join GitHub Discussions for questions
- **Email**: Contact the development team

## 🔄 Changelog

### v3.0.0 (Current)

- Complete rewrite with Next.js 15 and Hono
- Advanced AI content generation with Mastra
- Comprehensive LinkedIn integration
- Full post management system
- User authentication and profiles
- Scheduling and calendar features

### v2.0.0

- Basic content generation
- Simple LinkedIn posting
- User authentication

### v1.0.0

- Initial release
- Basic post generation

---

**ContentFlow v3** - Empowering professionals with AI-driven LinkedIn content creation and management.
