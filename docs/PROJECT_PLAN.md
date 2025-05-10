# Ticket Sales Platform Specification

## Overview

A modern, flexible ticket sales platform built with TypeScript that addresses the limitations of existing solutions. This platform will offer open APIs, extensive integrations, plugin capabilities, and white-labeling while allowing customers to choose their payment providers.

## Core Value Propositions

- **Open and Flexible**: Extensive API access and integration options
- **Choice of Payment Providers**: No forced payment gateway
- **Cloud Service with Self-Hosting Option**: SaaS model with open-source core
- **Plugin Marketplace**: Extensible functionality
- **White-Labeling**: Full customization of branding
- **Multi-Tenant Architecture**: Support for multiple venues/departments
- **Modern Tech Stack**: TypeScript, Node.js, React ecosystem

## Technology Stack

### Backend
- **Language**: TypeScript
- **Framework**: NestJS
- **Database**: PostgreSQL
- **Caching**: Redis
- **Search**: Meilisearch
- **Job Processing**: Bull queue with Redis

### Frontend
- **Framework**: Next.js
- **Styling**: Tailwind CSS
- **Animations**: Framer Motion
- **No-Code Editor**: Puck Editor integration
- **State Management**: React Query + Context API

### Infrastructure
- **Repository**: NX Monorepo
- **Container Orchestration**: Kubernetes for cloud offering
- **CI/CD**: GitHub Actions or GitLab CI
- **Monitoring**: Prometheus + Grafana
- **Logging**: ELK Stack

## Core Services

1. **PostgreSQL Database Service**
   - Primary data storage
   - Connection pooling via PgBouncer
   - Row-level security for multi-tenancy

2. **Redis Service**
   - Caching
   - Session storage
   - Real-time features
   - Job queues

3. **API Service (NestJS)**
   - Core business logic
   - REST and GraphQL APIs
   - Authentication and authorization

4. **Plugin Service (NestJS)**
   - Plugin execution environment
   - Plugin lifecycle management
   - Dynamic content serving

5. **Job Processing Service**
   - Background task execution
   - Scheduled jobs
   - Email and notification sending

6. **API Gateway Service**
   - Request routing
   - Rate limiting
   - Request transformation

7. **Admin Dashboard Application (Next.js)**
   - Administration interface
   - Plugin management
   - Reports and analytics
   - Customizable widget dashboard

8. **Storefront Application (Next.js)**
   - Customer-facing event listings
   - Ticket purchasing flow
   - White-labeled and customizable

9. **File Storage Service**
   - Default implementation built-in
   - Pluggable with S3-compatible storage

10. **Search Service (Meilisearch)**
    - Advanced search capabilities
    - Faceted search for events

11. **Notification Service**
    - Available through plugins
    - Email, SMS, push notifications

12. **Plugin Registry Service**
    - Plugin discovery
    - Version compatibility
    - Installation management

## NX Monorepo Structure

### Apps

1. **`api`** - NestJS core API service
2. **`plugin-service`** - NestJS service for plugins
3. **`admin`** - Next.js admin dashboard
4. **`storefront`** - Next.js customer-facing site
5. **`docs`** - Documentation site

### Core Libraries

```
libs/
  core/
    database/      # Database models and connections
    config/        # Configuration management
    logger/        # Logging utilities
    auth/          # Authentication/authorization
    errors/        # Error handling
    testing/       # Testing utilities
  
  domain/
    events/        # Event management logic
    tickets/       # Ticket management logic
    users/         # User management logic
    organizations/ # Organization/tenant management
    plugins/       # Plugin system logic
    dashboard-layouts/ # Dashboard layout management
  
  api/
    graphql/       # GraphQL schema and resolvers
    rest/          # REST controllers and DTOs
    webhooks/      # Webhook definitions and handlers
    dashboard/     # Dashboard API endpoints
  
  ui/
    components/    # Shared React components
    hooks/         # Custom React hooks
    styles/        # Styling utilities and themes
    layouts/       # Page layouts and containers
    forms/         # Form components and validation
    icons/         # Icon components
    dashboard-widgets/ # Dashboard widget system
  
  integrations/
    storage/       # File storage abstraction
    search/        # Search service integration
    notifications/ # Notification service abstractions
  
  plugins/
    sdk/           # Plugin development SDK
    registry/      # Plugin registry client
    extensions/    # Extension point definitions
    ui/            # Plugin UI components
  
  utils/
    dates/         # Date utilities
    formatting/    # String/number formatting
    validation/    # Input validation
```

### Tools
```
tools/
  generators/     # Custom NX generators
  scripts/        # Utility scripts
  docker/         # Docker configurations
```

## Plugin System Architecture

### Approach
The plugin system will use a **Dynamic Routing + Component Registry** approach, with consideration for a **Plugin Server** for more advanced use cases.

### Extension Points
Plugins can extend the platform through predefined extension points:

1. **Admin UI Extension Points**
   - Navigation items
   - Settings pages
   - Custom pages
   - Dashboard widgets

2. **Storefront Extension Points**
   - Checkout flow steps
   - Event display components
   - User profile sections

3. **API Extension Points**
   - Custom endpoints
   - GraphQL schema extensions
   - Webhooks

4. **Business Logic Extensions**
   - Payment gateways
   - Authentication providers
   - Ticket types
   - Reporting engines

### Plugin Registry
The platform will maintain a central registry of available plugins with:
- Metadata about each plugin
- Version compatibility information
- Installation/update/removal lifecycle management

### Dashboard Widget System

Plugins can register dashboard widgets that admins can add, remove, and rearrange:

1. **Widget Types**
   - Analytics widgets (charts, KPIs)
   - Action widgets (quick actions)
   - Status widgets (system health)
   - List widgets (recent events, orders)
   - Custom widgets

2. **Widget Features**
   - Configurable size constraints
   - User-specific settings
   - Drag-and-drop positioning
   - Responsive layouts

3. **Technical Implementation**
   - Widget registry system
   - React Grid Layout for positioning
   - Per-user layout storage
   - Widget container components

## Authentication & Security

1. **Authentication System**
   - JWT for stateless authentication
   - Support for multiple auth providers via plugins
   - Single Sign-On (SSO) capabilities

2. **Authorization**
   - Role-Based Access Control (RBAC)
   - Extensible permission system
   - Plugin-specific permissions

3. **Security Measures**
   - HTTPS everywhere
   - CSRF protection
   - Content Security Policy
   - Rate limiting
   - Input validation

## Multi-Tenancy Approach

A hybrid approach:
- Shared database with tenant IDs for most tables
- Row-level security in PostgreSQL
- Optional dedicated schemas for enterprise customers
- Tenant-specific configurations

## Core Features (Minimal Set)

### Event Management
- CRUD operations for events
- Ticketing configuration
- Event scheduling
- Attendee management

### User & Organization Management
- User authentication and profiles
- Role assignments
- Organization settings
- Team management

### Plugin System
- Plugin installation/removal
- Plugin marketplace
- Plugin settings
- Version management

### System Administration
- Tenant configuration
- Branding and theming
- API key management
- System health monitoring

## Development Workflow

1. **Setup**:
   - Initialize NX workspace
   - Create core apps and libraries
   - Set up Docker development environment

2. **First Milestone**:
   - Basic authentication
   - Event CRUD operations
   - Simple admin interface
   - Deployment pipeline

3. **Plugin System**:
   - Implement plugin registry
   - Define extension points
   - Create sample plugins
   - Dashboard widget system

4. **Marketplace & Distribution**:
   - Plugin marketplace
   - Self-hosting documentation
   - Cloud deployment infrastructure

## Additional Considerations

### API Design
- GraphQL API with Apollo Server
- REST endpoints for simple integrations
- Webhooks for event notifications
- Clear versioning strategy

### Developer Experience
- Plugin starter kit
- Comprehensive documentation
- Local development environment

### Deployment Options
- Docker containers
- Kubernetes for cloud
- Simple setup for self-hosting

## Business Model

- **Cloud Service**: Subscription-based pricing tiers
- **Self-Hosting**: Free open-source core with paid support options
- **Marketplace**: Revenue sharing for premium plugins
- **Enterprise**: Custom pricing for dedicated resources and support