# Module 6: Full-Stack Capstone Project

**Duration:** 8 weeks
**Commitment:** 1-2 hours/day
**Philosophy:** Build-Your-Own-X. No solutions provided. You build, you debug, you learn.

---

## Why a Capstone?

Building a complete project from scratch is fundamentally different from completing guided tutorials or smaller exercises. Here's why this capstone matters:

### Why Building a Complete Project Matters

- **Integration skills:** Smaller projects teach individual concepts. A capstone forces you to integrate authentication, database design, API development, state management, and deployment into one cohesive system. This integration is where real learning happens.
- **Decision fatigue practice:** In real jobs, you make hundreds of small decisions daily. A capstone gives you practice making and living with those decisions.
- **Debugging complex systems:** When something breaks in a full-stack app, the bug could be anywhere—frontend, backend, database, or the connections between them. Learning to trace issues across layers is an essential skill.
- **Ownership mentality:** This is your project. You can't blame the tutorial. You can't skip the hard parts. This ownership builds confidence.

### How This Differs from Smaller Projects

| Smaller Projects | Capstone Project |
|-----------------|------------------|
| Focus on one concept | Integrate many concepts |
| Guided structure | You define the structure |
| Isolated components | Connected systems |
| Hours to complete | Weeks to complete |
| Clear right answers | Trade-offs and decisions |

### What Employers Look For in Portfolio Projects

- **Completion:** A finished, deployed project beats ten half-done experiments
- **Problem-solving evidence:** Your commit history, README, and code comments show how you think
- **Real-world patterns:** Authentication, data relationships, error handling—the boring stuff that matters
- **Code quality:** Clean organization, consistent patterns, meaningful names
- **Communication:** Can you explain what you built and why?

### Why Deployment and Documentation Matter

Deployment proves you can ship. Many developers can code locally but struggle with environment variables, production databases, and CI/CD. Showing a live URL demonstrates you can deliver.

Documentation shows you think about others. Code without documentation is a liability. Writing clear READMEs, setup instructions, and architecture notes proves you're ready to work on a team.

---

## Overview

This capstone brings together everything from the course. You will architect, build, and deploy a complete full-stack application from scratch. Choose one of the three project options and deliver a portfolio-ready product.

---

## Week 1-2: Architecture & Planning

### Learning Objectives
- Translate an idea into technical requirements
- Design database schemas that scale
- Plan API contracts before writing code
- Create wireframes that guide development

### Topics

**Requirements Gathering**
- Define user stories and acceptance criteria
- Identify core features vs. nice-to-haves
- Establish MVP scope
- Document technical constraints

**Database Schema Design**
- Entity relationship diagrams
- Normalization principles
- Choosing data types
- Planning for relationships (one-to-many, many-to-many)
- Indexes and query optimization basics

**API Endpoint Planning**
- RESTful conventions
- Resource naming
- Request/response shapes
- Authentication requirements per endpoint
- Error response standards

**UI Wireframing**
- Low-fidelity sketches
- User flow diagrams
- Component hierarchy planning
- Responsive breakpoint considerations

**Tech Stack Decisions**
- Frontend framework (React)
- Backend framework (Node.js/Express or Next.js API routes)
- Database (PostgreSQL recommended)
- ORM choice (Prisma, Drizzle, or raw SQL)
- Authentication approach (JWT, sessions, OAuth)

**Project Setup**
- Monorepo vs. separate repositories
- Folder structure conventions
- Environment configuration
- Git workflow and branching strategy

### Labs

🔴 **Core** — **Lab 6.1: Requirements Document**
Write a complete requirements document for your chosen project. Include user stories, data models, and API endpoints. This document guides your entire build.

🔴 **Core** — **Lab 6.2: Database Schema**
Design your database schema. Create an ERD diagram. Write the SQL or Prisma schema file. Identify potential query patterns and plan indexes.

🔴 **Core** — **Lab 6.3: API Contract**
Document every API endpoint your application needs. Include request methods, paths, request bodies, response shapes, and authentication requirements.

🟡 **Recommended** — **Lab 6.4: Wireframes**
Create wireframes for every page in your application. Include mobile and desktop views. Annotate with component names.

### Weekly Review: Weeks 1-2

Take 15-20 minutes to reflect on your progress:

- **What did you accomplish?** List the planning artifacts you created. Are your requirements clear? Is your schema solid?
- **What blockers did you face?** Did you struggle with scope definition? Database relationships? Technology choices?
- **What would you do differently?** If you started over, what would you change about your planning process?

---

## Week 3-5: Full-Stack Build

### Learning Objectives
- Implement a production-ready database layer
- Build secure, well-structured APIs
- Connect frontend to backend seamlessly
- Make informed state management decisions

### Topics

**Database Setup and Migrations**
- Local database setup
- Migration files and version control
- Seeding development data
- Database connection pooling

**API Implementation with Authentication**
- Route organization
- Middleware patterns
- Password hashing and verification
- JWT creation and validation
- Protected route patterns
- Input validation and sanitization

**Frontend Scaffolding**
- Project structure for scale
- Routing setup
- Layout components
- Navigation patterns
- Authentication context/state

**Connecting Frontend to Backend**
- API client setup (fetch, axios, or React Query)
- Environment variables for API URLs
- Request/response interceptors
- Error handling patterns

**State Management Decisions**
- When to use local state
- When to lift state up
- Server state vs. client state
- Caching strategies
- Context vs. external libraries

**File Upload Handling**
- Multipart form data
- Backend file processing
- Cloud storage integration (S3, Cloudinary)
- Image optimization
- Progress indicators

### Labs

🔴 **Core** — **Lab 6.5: Database Layer**
Set up your database. Write migrations. Create seed data. Verify your schema works with sample queries.

🔴 **Core** — **Lab 6.6: Authentication System**
Implement complete user authentication. Registration, login, logout, and password reset. Protect routes that require authentication.

🔴 **Core** — **Lab 6.7: Core API Endpoints**
Build out your main feature APIs. Follow your API contract. Write at least 10 endpoints covering CRUD operations for your main resources.

🔴 **Core** — **Lab 6.8: Frontend Foundation**
Scaffold your React application. Implement routing, layouts, and navigation. Create the authentication flow UI.

🔴 **Core** — **Lab 6.9: API Integration**
Connect your frontend to your backend. Implement at least 5 complete features end-to-end. Handle loading and error states.

### Weekly Review: Weeks 3-5

Take 15-20 minutes to reflect on your progress:

- **What did you accomplish?** Which features are working end-to-end? What percentage of your MVP is complete?
- **What blockers did you face?** Authentication issues? Database queries? State management confusion? API integration problems?
- **What would you do differently?** Would you structure your code differently? Choose different libraries? Plan your time differently?

---

## Week 6-7: Polish & Quality

### Learning Objectives
- Handle errors gracefully across the stack
- Create smooth user experiences with loading states
- Validate data at every layer
- Write tests that provide confidence

### Topics

**Error Handling**
- Backend error middleware
- Consistent error response format
- Frontend error boundaries
- User-friendly error messages
- Logging and monitoring basics

**Loading States and Optimistic Updates**
- Skeleton screens vs. spinners
- Optimistic UI patterns
- Rollback on failure
- Perceived performance

**Form Validation**
- Client-side validation
- Server-side validation
- Validation libraries (Zod, Yup)
- Displaying validation errors
- Accessible form feedback

**Responsive Design**
- Mobile-first approach
- Breakpoint strategy
- Touch-friendly interactions
- Testing across devices

**Writing Tests**
- Unit testing components
- Integration testing API endpoints
- Testing authentication flows
- Mocking external services
- Test coverage goals

**Performance Considerations**
- Database query optimization
- API response times
- Frontend bundle size
- Image optimization
- Lazy loading

### Labs

🔴 **Core** — **Lab 6.10: Error Handling Audit**
Review every API endpoint and frontend interaction. Ensure errors are caught and displayed appropriately. No unhandled promise rejections. No white screens of death.

🟡 **Recommended** — **Lab 6.11: Loading State Polish**
Add loading indicators to every async operation. Implement at least one optimistic update. Test on slow network conditions.

🔴 **Core** — **Lab 6.12: Form Validation**
Implement validation for every form in your application. Validate on both client and server. Display clear error messages.

🟡 **Recommended** — **Lab 6.13: Responsive Audit**
Test your application at mobile, tablet, and desktop sizes. Fix layout issues. Ensure touch interactions work properly.

🟢 **Stretch** — **Lab 6.14: Test Suite**
Write tests for your application. Cover authentication flows, main feature CRUD operations, and edge cases. Aim for meaningful coverage, not just high numbers.

### Weekly Review: Weeks 6-7

Take 15-20 minutes to reflect on your progress:

- **What did you accomplish?** How polished does your app feel? What quality improvements did you make?
- **What blockers did you face?** Edge cases you didn't anticipate? Responsive design challenges? Testing difficulties?
- **What would you do differently?** Would you prioritize polish earlier? Write tests sooner? Focus on different quality aspects?

---

## Week 8: Deploy & Document

### Learning Objectives
- Manage environment configuration securely
- Deploy full-stack applications to production
- Set up basic CI/CD pipelines
- Present your work professionally

### Topics

**Environment Variables and Secrets**
- Local vs. production configuration
- Secret management best practices
- Environment variable validation
- Never commit secrets

**Production Deployment**
- Frontend deployment (Vercel)
- Backend/database deployment (Railway)
- Domain configuration
- SSL certificates
- Environment variable setup in production

**CI/CD Basics**
- GitHub Actions introduction
- Automated testing on push
- Automated deployment on merge
- Build status badges

**README and Documentation**
- Project overview
- Screenshots and demos
- Local development setup
- Environment variable documentation
- Architecture decisions
- Known limitations

**Portfolio Presentation**
- Writing about your project
- Highlighting technical decisions
- Explaining challenges overcome
- Recording demo videos

### Labs

🔴 **Core** — **Lab 6.15: Production Deployment**
Deploy your application. Frontend on Vercel, backend and database on Railway. Verify everything works in production. Set up a custom domain if available.

🟢 **Stretch** — **Lab 6.16: CI/CD Pipeline**
Create a GitHub Actions workflow. Run tests on every pull request. Deploy automatically on merge to main.

🔴 **Core** — **Lab 6.17: Documentation**
Write a complete README. Include screenshots. Document setup instructions. Make it portfolio-ready.

🟡 **Recommended** — **Lab 6.18: Final Presentation**
Record a 3-5 minute demo video. Write a blog post or portfolio page about your project. Share your work.

### Weekly Review: Week 8

Take 15-20 minutes to reflect on your progress:

- **What did you accomplish?** Is your app deployed and accessible? Is your documentation complete?
- **What blockers did you face?** Deployment configuration issues? Environment variable problems? Documentation gaps?
- **What would you do differently?** Would you deploy earlier? Document as you go? Set up CI/CD sooner?

---

## Capstone Project Options

Choose one project. Each has specific requirements. You define the implementation details.

---

### Option A: Task Management App (Trello-like)

#### Complexity Tiers

**Tier 1: MVP (Minimum Viable Product)**
Focus on core functionality only:
- User registration and login
- Create and delete boards
- Create, edit, and delete lists
- Create, edit, and delete cards
- Basic card ordering (no drag-and-drop required)
- Simple, functional UI

**Tier 2: Standard (Full Requirements)**
Everything in Tier 1, plus:
- Full drag-and-drop for cards and lists
- Card details with descriptions and due dates
- Board permissions and sharing
- Responsive design
- Loading states and error handling

**Tier 3: Advanced (Extended Features)**
Everything in Tier 2, plus:
- Real-time collaboration with WebSockets
- Card labels and filtering
- Activity history/audit log
- Card attachments and file uploads
- Email notifications for due dates
- Keyboard shortcuts

#### Core Requirements

*User Authentication*
- User registration with email and password
- User login and logout
- Protected routes for authenticated users
- User profile with editable details

*Boards*
- Create, read, update, delete boards
- Board ownership and permissions
- Board listing for authenticated user

*Lists*
- Create, read, update, delete lists within boards
- List ordering within boards
- Drag and drop list reordering

*Cards*
- Create, read, update, delete cards within lists
- Card details (title, description, due date)
- Drag and drop cards between lists
- Card ordering within lists

*Optional: Real-Time Updates*
- Live updates when collaborators make changes
- WebSocket or polling implementation

**Technical Considerations**
- Drag and drop library selection
- Optimistic updates for smooth UX
- Efficient re-rendering on reorder
- Position/order field strategy in database

---

### Option B: E-Commerce Storefront

#### Complexity Tiers

**Tier 1: MVP (Minimum Viable Product)**
Focus on core shopping flow:
- Product listing page with basic info
- Product detail pages
- Add to cart functionality
- Simple cart page with totals
- Basic checkout form (no payment processing)
- Order confirmation page

**Tier 2: Standard (Full Requirements)**
Everything in Tier 1, plus:
- Category filtering and search
- User accounts with order history
- Cart persistence across sessions
- Multi-step checkout flow
- Form validation throughout
- Responsive design

**Tier 3: Advanced (Extended Features)**
Everything in Tier 2, plus:
- Stripe payment integration (test mode)
- Admin dashboard for product management
- Inventory tracking with low-stock alerts
- Wishlist functionality
- Product reviews and ratings
- Email order confirmations
- Discount codes and promotions

#### Core Requirements

*Product Catalog*
- Product listing page
- Product detail pages
- Category filtering
- Search functionality
- Price and attribute filtering
- Pagination or infinite scroll

*Shopping Cart*
- Add items to cart
- Update quantities
- Remove items
- Cart persistence (localStorage or database)
- Cart total calculation

*Checkout Flow*
- Shipping information form
- Order summary review
- Mock payment processing
- Order confirmation

*User Accounts*
- User registration and login
- Order history page
- Saved addresses (optional)

**Technical Considerations**
- Inventory management basics
- Cart state management
- Form validation across checkout steps
- Guest checkout vs. required accounts

---

### Option C: Social Platform

#### Complexity Tiers

**Tier 1: MVP (Minimum Viable Product)**
Focus on core social features:
- User registration and login
- Basic profile page
- Create and view text posts
- Chronological feed of all posts
- Basic pagination

**Tier 2: Standard (Full Requirements)**
Everything in Tier 1, plus:
- Editable profiles with avatars
- Follow/unfollow system
- Personalized feed (following only)
- Comments on posts
- Post editing and deletion
- Responsive design

**Tier 3: Advanced (Extended Features)**
Everything in Tier 2, plus:
- Image uploads for posts
- Nested comment replies
- Like/reaction system
- Real-time notifications
- Direct messaging
- Hashtags and trending topics
- User search and discovery
- Privacy settings (public/private accounts)

#### Core Requirements

*User Profiles*
- User registration and login
- Profile page with bio and avatar
- Editable profile information
- Public profile viewing

*Posts*
- Create text posts
- Image uploads (optional)
- Post editing and deletion
- Post timestamps

*Comments*
- Comment on posts
- Comment editing and deletion
- Nested replies (optional)

*Follow System*
- Follow and unfollow users
- Followers and following counts
- Following list view

*Activity Feed*
- Chronological feed of followed users' posts
- Pagination or infinite scroll
- Pull-to-refresh pattern

**Technical Considerations**
- Feed query optimization
- Image upload and storage
- Notification patterns (optional)
- Privacy considerations

---

## Portfolio Requirements

Your capstone must meet these standards:

**Deployed and Live**
- Application accessible via public URL
- Both frontend and backend functional
- No broken features in production

**Clean README**
- Project title and description
- Screenshots or GIF demos
- Technology stack listed
- Local development setup instructions
- Environment variables documented
- Live demo link included

**Clear Code Organization**
- Logical folder structure
- Consistent naming conventions
- Separation of concerns
- No commented-out code
- Meaningful commit history

**Demonstrates Full-Stack Skills**
- Frontend: React, routing, state management, API integration
- Backend: REST API, authentication, database operations
- Database: Schema design, relationships, migrations
- DevOps: Deployment, environment configuration

---

## Final Deliverables

1. **Live Application**
   - Deployed on Vercel (frontend) + Railway (backend/database)
   - All core features functional
   - Responsive on mobile and desktop

2. **GitHub Repository**
   - Clean commit history
   - Comprehensive README
   - No exposed secrets

3. **Documentation**
   - Setup instructions
   - Architecture overview
   - Screenshots

4. **Presentation Materials**
   - Demo video (3-5 minutes)
   - Portfolio page or blog post

---

## Evaluation Criteria

Your capstone demonstrates competency through:

- **Functionality:** Does the application work as intended?
- **Code Quality:** Is the code readable, organized, and maintainable?
- **User Experience:** Is the application intuitive and responsive?
- **Technical Depth:** Does it demonstrate full-stack understanding?
- **Documentation:** Can someone else understand and run the project?

---

## Recommended Resources

### Deployment Guides
- [Vercel Documentation](https://vercel.com/docs) — Frontend deployment
- [Railway Documentation](https://docs.railway.app/) — Backend and database deployment
- [Render Documentation](https://render.com/docs) — Alternative to Railway
- [PlanetScale Documentation](https://planetscale.com/docs) — Serverless MySQL alternative
- [Supabase Documentation](https://supabase.com/docs) — PostgreSQL with built-in auth

### Portfolio Presentation Tips
- **Show, don't tell:** Screenshots and demos are more compelling than descriptions
- **Lead with the problem:** Explain what problem your app solves before diving into features
- **Highlight technical decisions:** Explain why you chose your tech stack, not just what it is
- **Be honest about trade-offs:** Discussing what you'd do differently shows maturity
- **Make it easy to run:** Clear setup instructions reduce friction for reviewers

### Code Review Checklist
Before considering your capstone complete, verify:

- [ ] No console.log statements left in production code
- [ ] No commented-out code
- [ ] Environment variables documented (without actual values)
- [ ] Error handling for all API calls
- [ ] Loading states for all async operations
- [ ] Form validation on client and server
- [ ] Responsive design tested on mobile
- [ ] No TypeScript errors or warnings
- [ ] README includes screenshots
- [ ] All features work in production

### System Design Basics
Understanding these concepts will help you discuss your project intelligently:

- **Separation of concerns:** Why frontend, backend, and database are separate
- **REST principles:** Why your API is structured the way it is
- **Authentication flow:** How tokens/sessions work in your app
- **Database relationships:** Why you structured your schema that way
- **State management:** Why you chose your approach to managing data
- **Caching strategy:** How you handle repeated data fetches

### Additional Learning Resources
- [The Twelve-Factor App](https://12factor.net/) — Best practices for web apps
- [REST API Design Best Practices](https://restfulapi.net/) — API design principles
- [Web.dev](https://web.dev/) — Performance and best practices from Google
- [Testing Library Documentation](https://testing-library.com/docs/) — Testing React apps

---

## Tips for Success

1. **Start with MVP.** Build the minimum viable version first. Add features after core functionality works.

2. **Commit often.** Small, frequent commits make debugging easier and show your progress.

3. **Test in production early.** Deploy early and often. Don't wait until the end to discover deployment issues.

4. **Document as you go.** Write README sections as you build. Don't leave documentation for the last day.

5. **Ask for feedback.** Share your progress with peers. Fresh eyes catch issues you miss.

6. **Manage scope.** It's better to have a polished simple app than a broken complex one.

---

## Final Self-Assessment

Before considering yourself "graduated" from this course, honestly answer these questions. If you can't confidently answer "yes" to most of them, revisit the relevant areas.

### Technical Readiness

1. **Can you explain your architecture decisions?**
   - Why did you choose your tech stack?
   - Why is your database schema structured this way?
   - What trade-offs did you make and why?

2. **Can you debug a production issue?**
   - If your deployed app breaks, can you trace the issue?
   - Do you know how to check logs, test API endpoints, and verify database state?

3. **Can you add a new feature end-to-end?**
   - If asked to add a new feature, can you implement it from database to UI?
   - Do you understand how all the layers connect?

4. **Can you explain your authentication flow?**
   - How does a user go from registration to authenticated requests?
   - Where are tokens stored? How are they validated?

### Professional Readiness

5. **Can you walk someone through your code?**
   - Could you explain your codebase to another developer?
   - Can you justify your organizational decisions?

6. **Can you discuss what you'd do differently?**
   - What would you change if you started over?
   - What did you learn about your own development process?

### Portfolio Readiness

- [ ] Your app is deployed and accessible
- [ ] Your README is complete with screenshots
- [ ] You can demo your app in under 5 minutes
- [ ] You can discuss technical decisions confidently
- [ ] You can explain challenges you overcame

---

**Final Deploy:** Complete full-stack application on Vercel + Railway

You've learned the pieces. Now build something real.
