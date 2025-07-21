# ScamShield - Fraud Detection Application

## Overview

ScamShield is a comprehensive web application designed to help users detect and report suspicious online scams. The application allows users to analyze various types of potentially fraudulent content including URLs, phone numbers, emails, bank details, and images. It combines AI-powered analysis with community-driven reporting to provide risk assessments and protective recommendations.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Architecture Pattern
The application follows a full-stack monorepo architecture with a clear separation between client and server components. It uses a modern React frontend with Express.js backend, implemented in TypeScript for type safety across the entire stack.

### Technology Stack
- **Frontend**: React 18 with TypeScript, Vite for bundling
- **Backend**: Express.js with TypeScript
- **Database**: PostgreSQL with Drizzle ORM
- **UI Framework**: Tailwind CSS with shadcn/ui components
- **State Management**: TanStack Query for server state
- **AI Integration**: OpenAI GPT-4o for content analysis
- **File Uploads**: Multer for handling image uploads

## Key Components

### Frontend Architecture
- **Component-based UI**: Built with React and shadcn/ui component library
- **Routing**: Uses Wouter for lightweight client-side routing
- **Styling**: Tailwind CSS with custom design tokens for branding
- **Forms**: React Hook Form with Zod validation
- **State Management**: TanStack Query for API data fetching and caching

### Backend Architecture
- **API Layer**: RESTful endpoints using Express.js
- **Data Access**: Drizzle ORM for type-safe database operations
- **File Handling**: Multer middleware for image upload processing
- **AI Services**: Dedicated service layer for OpenAI integration
- **Analysis Services**: Modular services for domain, phone, and email analysis

### Database Schema
The application uses PostgreSQL with three main tables:
- **users**: User authentication and management
- **scam_reports**: Community-driven scam reports with risk scores and metadata
- **scan_analysis**: Individual scan results linked to user sessions

### Authentication & Authorization
Currently implements a basic user system with username/password authentication. Session management is handled through the storage layer.

## Data Flow

### Scan Analysis Flow
1. User submits content through the frontend scanner form
2. Backend validates input and determines analysis type
3. Multiple analysis services run in parallel:
   - Domain analysis for URLs
   - AI-powered content analysis via OpenAI
   - Cross-reference with community database
4. Results are aggregated into a risk assessment
5. Analysis is stored for future reference
6. Frontend displays comprehensive risk report

### Community Reporting Flow
1. Analysis results can be anonymously contributed to community database
2. Similar content is flagged when detected in future scans
3. Community can mark reports as helpful
4. Verified reports carry higher weight in risk calculations

### Real-time Features
- Live search through community reports
- Instant risk assessment display
- Progressive enhancement for file uploads

## External Dependencies

### AI Services
- **OpenAI GPT-4o**: Primary AI engine for content analysis and scam detection
- Configured for JSON-structured responses for consistent parsing

### Database
- **PostgreSQL**: Primary data store configured via Drizzle
- **Neon Database**: Cloud PostgreSQL provider (based on connection string pattern)

### Third-party Libraries
- **Radix UI**: Accessible component primitives
- **Lucide React**: Icon library
- **Date-fns**: Date manipulation utilities
- **Class Variance Authority**: CSS class management

## Deployment Strategy

### Development Environment
- **Vite Dev Server**: Hot module replacement for frontend development
- **tsx**: TypeScript execution for backend development
- **Integrated Development**: Single command runs both frontend and backend

### Production Build
- **Frontend**: Vite builds optimized static assets
- **Backend**: esbuild bundles Node.js server application
- **Static Serving**: Express serves frontend assets in production

### Environment Configuration
- Database URL required via environment variables
- OpenAI API key required for AI analysis features
- Graceful degradation when AI services unavailable

### File Structure
```
├── client/          # React frontend application
├── server/          # Express.js backend
├── shared/          # Shared TypeScript schemas and types
├── migrations/      # Database migration files
└── dist/           # Production build output
```

### Scalability Considerations
- Stateless backend design for horizontal scaling
- Database connection pooling via Drizzle
- Caching strategy through TanStack Query
- Optimistic UI updates for better user experience

The application is designed to be easily deployable on platforms like Replit, with configuration files supporting both development and production environments.