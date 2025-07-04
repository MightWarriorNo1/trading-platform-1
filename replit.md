# replit.md

## Overview

This repository contains a full-stack web application called "Project Resolve AI" - an AI-powered legal support platform specifically designed for Australian tradespeople. The application helps users manage legal cases, contracts, and provides AI-powered legal guidance for payment disputes and other trade-related legal issues.

## System Architecture

The application follows a modern full-stack architecture:

- **Frontend**: React 18 with TypeScript, using Vite as the build tool
- **Backend**: Express.js server with TypeScript
- **Database**: Supabase PostgreSQL with direct Supabase client
- **Authentication**: Supabase Auth with JWT middleware
- **Styling**: Tailwind CSS with shadcn/ui components
- **File Storage**: Local file system with multer for uploads
- **External Services**: Optional integrations for OpenAI, Stripe, and email services

## Key Components

### Frontend Architecture
- **React Router**: Using wouter for client-side routing
- **State Management**: TanStack Query (React Query) for server state
- **UI Components**: shadcn/ui component library with Radix UI primitives
- **Forms**: React Hook Form with Zod validation
- **Styling**: Tailwind CSS with custom design system

### Backend Architecture
- **API Server**: Express.js with TypeScript
- **Database Layer**: Drizzle ORM with PostgreSQL
- **Authentication**: Supabase Auth with JWT tokens
- **File Handling**: Multer for file uploads and storage
- **Email Service**: Nodemailer (optional, configurable)
- **AI Integration**: OpenAI API (optional, gracefully degrades)

### Database Schema
- **Users**: Extended user profiles with subscription and role management
- **Applications**: Initial form submissions from potential clients
- **Cases**: Legal case management with timeline tracking
- **Contracts**: Contract creation and management
- **Documents**: File attachment system for cases and contracts
- **Timeline Events**: Activity tracking for cases and contracts

## Data Flow

1. **User Registration/Login**: Handled by Supabase Auth
2. **Application Submission**: Anonymous users can submit initial applications
3. **Case Creation**: Authenticated users can create detailed legal cases
4. **Contract Management**: Users can create and manage contracts
5. **Document Upload**: Files can be attached to cases and contracts
6. **AI Analysis**: Optional OpenAI integration for case analysis and strategy generation
7. **Payment Processing**: Optional Stripe integration for subscription management

## External Dependencies

### Required Services
- **PostgreSQL Database**: For data persistence
- **Supabase**: For authentication and user management

### Optional Services (Graceful Degradation)
- **OpenAI API**: For AI-powered legal analysis and strategy generation
- **Stripe**: For payment processing and subscription management
- **SMTP Server**: For email notifications (Nodemailer)
- **SendGrid**: Alternative email service

### Environment Variables
- `DATABASE_URL`: PostgreSQL connection string
- `VITE_SUPABASE_URL`: Supabase project URL
- `VITE_SUPABASE_ANON_KEY`: Supabase anonymous key
- `SUPABASE_SERVICE_ROLE_KEY`: Supabase service role key
- `OPENAI_API_KEY`: OpenAI API key (optional)
- `STRIPE_SECRET_KEY`: Stripe secret key (optional)
- `VITE_STRIPE_PUBLIC_KEY`: Stripe publishable key (optional)
- `SESSION_SECRET`: Express session secret
- Email configuration (optional): `SMTP_HOST`, `SMTP_USER`, `SMTP_PASS`, etc.

## Deployment Strategy

### Development
- Uses Vite dev server for frontend
- Express server with hot reload via tsx
- PostgreSQL database (can be local or remote)

### Production Build
- Frontend: Vite builds static assets to `dist/public`
- Backend: esbuild bundles server code to `dist/index.js`
- Static files served by Express in production

### Replit Configuration
- Configured for autoscale deployment
- Uses Node.js 20 with PostgreSQL 16
- Port 5000 for development, external port 80 for production
- Workflow automation for easy deployment

### Key Features
- **Responsive Design**: Mobile-first approach with Tailwind CSS
- **Progressive Enhancement**: Core functionality works without optional services
- **File Upload System**: Supports documents, images, and PDFs
- **Role-Based Access**: User, moderator, and admin roles
- **Subscription Management**: Strategy packs and monthly subscriptions
- **AI-Powered Analysis**: Optional legal case analysis and strategy generation
- **Calendar Integration**: Full Google Calendar and Microsoft Outlook synchronization with OAuth 2.0 authentication

## Changelog

Changelog:
- June 15, 2025. Initial setup
- June 15, 2025. Completed Supabase migration and fixed 403 authentication errors in case/contract creation
- June 17, 2025. Completely resolved 403 authentication errors by implementing direct database storage layer, fixing timestamp handling in Drizzle ORM, and updating validation schemas. System now successfully creates cases and contracts with proper user authentication.
- June 17, 2025. Completed full Supabase migration - converted entire database architecture from hybrid PostgreSQL/Drizzle to pure Supabase client implementation. All database operations now use Supabase directly with proper field name mapping between frontend camelCase and database snake_case. Authentication and database operations are now unified under Supabase.
- June 17, 2025. Fixed document upload workflow - created comprehensive SQL setup for missing tables (timeline_events, documents, applications), implemented complete file upload endpoints with proper user authentication and field mapping, added multer configuration for secure file handling. Created supabase_timeline_events_table.sql for database table creation.
- June 18, 2025. Major architectural cleanup - consolidated entire project to use Supabase exclusively for authentication, authorization, and database operations. Removed redundant authentication systems (replitAuth.ts, auth-middleware.ts, direct-storage.ts, storage.ts) and route files (clean-routes.ts, case-routes.ts, contract-routes.ts, file-upload-routes.ts, routes.ts). Unified all API endpoints under supabase-routes.ts with consistent JWT token authentication. Fixed file upload authentication by ensuring proper Authorization header transmission from frontend to backend. System now uses single, clean Supabase-based architecture throughout.
- June 18, 2025. Implemented comprehensive micro-interaction animation system throughout the application to enhance user engagement. Added custom CSS animations (fadeIn, slideIn, pulse, bounce, shake, glow) with utility classes for buttons, cards, and interactive elements. Enhanced dashboard with staggered animations, hover effects, and smooth transitions. Applied animations to file upload components, navigation elements, stats cards, timeline events, and all interactive buttons. System includes card hover effects, button lift animations, icon bounce effects, and loading state animations for improved user experience.
- June 19, 2025. Completed comprehensive Google/Outlook calendar integration with full OAuth 2.0 authentication. Implemented CalendarService with Google Calendar API and Microsoft Graph integration for bidirectional synchronization. Added calendar_integrations and calendar_events database tables with complete CRUD operations. Created frontend calendar management components including integration settings, event creation forms, and calendar dashboard. Added dedicated /calendar route with comprehensive calendar management interface. Users can now connect external calendars, sync case deadlines, create events, and manage calendar settings seamlessly.
- June 19, 2025. Fixed calendar integration OAuth workflow - resolved Google OAuth redirect_uri parameter issue and missing calendar database tables. Updated OAuth flow to use popup-based authentication with postMessage communication for secure token exchange. Created supabase-calendar-tables.sql migration script for calendar database setup. Calendar integration now gracefully handles missing tables and provides proper error handling. Ready for Google Cloud Console OAuth configuration and Supabase table creation.
- June 19, 2025. Implemented comprehensive admin access layer with complete backend and frontend infrastructure. Created AdminService with dashboard statistics, user activity monitoring, notification system, and document review capabilities. Added admin-only routes for reviewing/editing AI-generated PDFs before client delivery, monitoring user signups and case activity, and managing system notifications. Built responsive admin dashboard with real-time notifications, document review modal with JSON editing, enhanced navigation with notification bar, and role-based access controls. System includes admin promotion functionality, activity timeline tracking, and comprehensive system health monitoring.
- June 19, 2025. Completed full calendar sync with Google/Outlook integration featuring comprehensive bidirectional synchronization. Enhanced CalendarService with bulk case sync, external calendar import, real-time updates synchronization, and comprehensive deadline event creation. Added CalendarSyncDashboard with live sync status monitoring, integration management, and automated progress tracking. Implemented enhanced API endpoints for bidirectional sync operations including bulk case sync, external calendar import, update synchronization, and sync status monitoring. System now provides complete calendar integration with automated case deadline creation, follow-up reminders, milestone tracking, and real-time synchronization between external calendars and the platform.
- June 20, 2025. Resolved critical file upload/download workflow issues including "Invalid document ID" and "Unknown File" errors. Fixed field mapping inconsistencies between database (snake_case) and frontend (camelCase) throughout the application. Corrected document download authentication with proper Bearer token handling in API endpoints. Added logo navigation functionality to redirect to landing page when clicked. Updated document preview, enhanced file upload, and case detail components for proper document handling. Fixed authentication flow for document downloads using Supabase session tokens. System now provides seamless file upload, preview, and download functionality with proper user permissions and error handling.
- June 20, 2025. Implemented email/password admin authentication system replacing role-based access. Created dedicated AdminAuthService with session management for specific admin credentials (hello@projectresolveai.com / helloprojectresolveai). Added admin login page at /admin-login route with secure session-based authentication. Updated all admin API endpoints to use new email/password authentication middleware instead of role checks. Admin sessions expire after 24 hours with automatic cleanup. System now provides secure admin access through dedicated login credentials rather than user role promotion.
- June 20, 2025. Completed comprehensive admin authentication workflow debugging and implementation. Fixed cookie parser integration, resolved session validation issues, and established complete admin authentication flow. Added AdminProtectedRoute component for frontend route protection, useAdminAuth hook for admin state management, and verified end-to-end admin login workflow. Admin authentication system now fully operational with proper session management, cookie handling, and route protection. Admins can access system via "Admin Access" link in footer → /admin-login → admin dashboard with full functionality.
- June 20, 2025. Migrated admin authentication to full Supabase Auth integration with database-stored sessions. Updated AdminAuthService to use Supabase Auth for login validation and admin role checking via user metadata. Created supabase-admin-tables.sql migration script for admin_sessions table and RLS policies. Implemented smart routing logic to automatically redirect authenticated admins to /admin dashboard instead of landing page. Admin system now uses proper Supabase Auth with persistent sessions and role-based access control.
- June 22, 2025. Completed comprehensive migration to Supabase Storage for all file uploads and downloads throughout the project. Replaced local multer-based file storage with cloud-based Supabase Storage system featuring private buckets, RLS policies, signed URLs, and organized folder structure. Created SupabaseStorageService backend class and SupabaseStorageClient frontend integration. Updated all file upload/download routes and components to use new storage system. Added supabase-storage-migration.sql for database schema updates. System now provides scalable, secure cloud file storage with proper authentication and user isolation.
- June 23, 2025. Created comprehensive contract detail page mirroring case detail functionality with full Supabase integration. Implemented five-tab structure (Overview, Analysis, Strategy, Documents, Timeline) with complete document upload/preview system, timeline management, note addition, and AI analysis display. Fixed calendar tab white screen issue in dashboard by adding calendar overview content with integration status and upcoming events. Updated admin authentication to use hardcoded credentials (hello@projectresolveai.com / helloprojectresolveai) instead of Supabase Auth integration. Contract detail page includes progress tracking, contract value display, party details, terms overview, and comprehensive file management with proper TypeScript typing and error handling.

## User Preferences

Preferred communication style: Simple, everyday language.