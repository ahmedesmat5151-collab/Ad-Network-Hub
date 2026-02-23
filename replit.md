# Souq Ads Network

## Overview
Souq Ads Network is a digital advertising platform connecting advertisers with mobile app publishers. It enables advertisers to create and manage ad campaigns using AI-generated content (images, audio, cinematic videos) and offers publishers tools to monetize their apps through ad display. The platform includes an admin dashboard for campaign approval and performance analytics. Key capabilities include a pay-per-use AI credits system, enhanced geographic targeting, granular user permissions, a landing page builder, multi-provider payment system with NBE MPGS integration, and comprehensive user authentication. It also features a cinematic video ad creator, an AI support chatbot, social media link management for publishers, and advanced SEO and analytics. Monetization relies on CPM/CPC models with budget management and a sophisticated targeting system. An anti-fraud system and AI content moderation ensure platform integrity, alongside creator channels for content sharing and role-based access control.

## User Preferences
Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
The frontend uses React 18 with TypeScript and Vite for bundling. Routing is handled by Wouter, and server state management and caching are managed with TanStack Query. UI components are built using shadcn/ui on Radix UI primitives, styled with Tailwind CSS supporting light/dark modes and CSS variables. Framer Motion is used for animations, and a custom hook-based internationalization system supports English and Arabic with RTL layout switching. File uploads utilize Uppy with AWS S3 integration via presigned URLs.

### Backend Architecture
The backend is built with Node.js and Express.js, written in TypeScript. It features RESTful API endpoints with Zod schema validation shared between the client and server. Drizzle ORM is used with PostgreSQL as the database. Shared schema definitions (`shared/schema.ts`) ensure type safety across the stack.

### AI Integrations
AI integrations, primarily via Replit AI Integrations, include OpenAI's gpt-image-1 for image generation, OpenAI TTS for text-to-speech, and OpenAI Whisper for speech-to-text. A full-duplex voice streaming system with AudioWorklet supports real-time audio playback for voice chat features.

### File Storage
Google Cloud Storage is used for file storage, accessed via Replit's sidecar service. A two-step presigned URL flow is implemented for secure uploads. Access control policies are metadata-based and stored with the objects.

### Build System
For development, a Vite dev server with HMR is used, proxied through Express. For production, the client is built with Vite, and the server is bundled into a single CJS file using esbuild, with core dependencies bundled to optimize cold start times.

### UI/UX Decisions
The platform utilizes Google Fonts (Cairo for Arabic, Inter for English) and various icon libraries (Lucide React, react-icons). The UI supports bilingual content (AR/EN) with RTL layout and themed light/dark modes.

### Technical Implementations
Key technical implementations include:
- **AI Usage Credits System**: A pay-per-use model for AI features with free quotas and credit management.
- **Enhanced Geographic Targeting**: A 4-level hierarchy (Governorate → City → Area → Street) for precise ad targeting.
- **Granular User Permissions**: Eight distinct permission types managed via an admin panel.
- **Landing Page Builder**: A template-based system for users to create and publish landing pages with draft/publish workflow.
- **Multi-Provider Payment System**: Admin configurable payment providers and per-app connection management.
- **NBE MPGS Payment Integration**: Direct integration with NBE MasterCard Payment Gateway Services supporting full and installment payments, with server-side validation and multiple payment methods (bank card, e-wallet, InstaPay).
- **User Authentication**: OpenID Connect via Replit (Google, GitHub, Apple, email/password) with PostgreSQL-backed sessions.
- **Cinematic Video Ad Creator**: Generates multi-scene MP4 videos using AI-generated images (DALL-E), AI voice narration, Ken Burns effects, and fade transitions.
- **AI Support Chatbot**: A floating widget using gpt-4o-mini with platform knowledge, streaming responses, and conversation persistence.
- **Social Media Links for Publishers**: Publishers can add and manage social media links for their apps with platform icons.
- **SEO Improvements**: JSON-LD schema, comprehensive meta tags, sitemap, robots.txt, and Open Graph tags.
- **Enhanced Notification System**: Various notification types for campaign status, budget, performance, and engagement.
- **Advanced Analytics Dashboard**: Provides key metrics, campaign status, budget utilization, pricing model distribution, and top-performing ads/cities/interests.
- **Monetization & Targeting Features**: CPM/CPC pricing, per-ad budget management, city and interest-based targeting with a scoring algorithm, publisher earnings tracking, and an ad serving algorithm.
- **Anti-Fraud System**: Rate limiting, fraud scoring based on IP, device fingerprint, view duration, and bot detection, with verified views and automatic flagging.
- **AI Content Moderation**: GPT-4o-mini rates content safety, auto-blocking high-risk content and sending others to an admin review queue.
- **Creator Channels**: Users can create image, video, and audio posts, follow creators, and engage with content (likes, comments).
- **Role-Based Access Control**: Roles (Publisher, Advertiser, Viewer, Admin) determine dashboard views and endpoint access.

## External Dependencies

### Database
- **PostgreSQL**: Primary database accessed via `DATABASE_URL`.
- **Drizzle Kit**: Used for database migrations.

### AI Services
- **OpenAI API**: Utilized for image generation, text-to-speech, and speech-to-text functionalities.

### Cloud Storage
- **Google Cloud Storage**: Used for object storage, integrated via Replit's sidecar service.

### Frontend Libraries
- **Google Fonts**: Cairo and Inter for internationalized typography.
- **Radix UI**: Provides headless UI primitives.
- **Lucide React**: Icon library.
- **react-icons**: Additional icon assets.

### Development Tools
- **Replit Plugins**: Used for runtime error overlay, cartographer, and dev banners.