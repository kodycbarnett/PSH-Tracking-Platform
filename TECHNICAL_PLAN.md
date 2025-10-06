# PSH Application Tracking Platform - Technical Implementation Plan

## Project Overview
An intelligent web-based Kanban platform to track housing applicants through the complex PSH (Permanent Supportive Housing) process in Portland, Oregon. The system replaces email chains and spreadsheet tracking with centralized visibility, process intelligence, and automated insights for all stakeholders.

### Vision
Transform PSH application tracking from a manual, fragmented process into an intelligent system that not only tracks current status but actively identifies bottlenecks, predicts delays, and provides actionable insights to optimize the entire workflow for faster, more reliable housing placements.

## Core Requirements

### Essential Features
- **Intelligent Kanban Board**: Visual workflow with bidirectional process tracking
- **Stage-Specific Contextual Notes**: Smart prompts that capture structured data while feeling natural
- **Process Analytics**: Timeline visualization, bottleneck identification, and optimization insights
- **Multi-Stakeholder Dashboards**: Tailored views for Property Managers, Case Managers, JOHS Staff, and Applicants
- **Automated Insights**: Claude API integration for process summaries and recommendations

### System Capabilities
- **Bidirectional Tracking**: Handle forward progress and bounce-back scenarios with contextual reasoning
- **Document Intelligence**: Track required documents per stage with reuse optimization (e.g., Tax Credit docs → HF Intake)
- **Microsoft Graph Integration**: Outlook email automation with template-based communications
- **Real-time Notifications**: Stage transitions trigger appropriate stakeholder alerts
- **Data Export**: Comprehensive reporting for compliance and process improvement
- **Client Portal**: Self-service applicant interface with transparency and document upload

## Technology Stack

### Frontend
- **Framework**: React.js with TypeScript
- **UI Library**: Tailwind CSS for clean, accessible design
- **State Management**: React Context for stage transitions and real-time updates
- **Drag & Drop**: react-beautiful-dnd for Kanban functionality
- **File Upload**: react-dropzone for document handling
- **Charts/Analytics**: Chart.js or D3.js for timeline visualizations
- **Microsoft Graph**: @azure/msal-react for Outlook integration
- **Responsive**: Mobile-first design for tablet/phone access

### Backend
- **Runtime**: Node.js
- **Framework**: Express.js with TypeScript
- **Database**: PostgreSQL (structured data) + Supabase for real-time features
- **Authentication**: JWT tokens with role-based access + Azure AD integration
- **Email**: Microsoft Graph API for Outlook integration
- **File Storage**: Supabase Storage or AWS S3 for document storage
- **AI Integration**: Claude API for automated summaries and insights
- **API**: RESTful endpoints with real-time WebSocket connections

### Data & Analytics
- **Time Tracking**: Precise stage duration measurement with timezone handling
- **Export Capabilities**: CSV, Excel, PDF reports for stakeholder consumption  
- **Process Intelligence**: Pattern recognition for common delay causes
- **Predictive Analytics**: Timeline estimation based on historical data
- **Dashboard Engine**: Configurable widgets for different stakeholder views

### Infrastructure
- **Hosting**: Vercel (frontend) + Railway/Render (backend) for rapid deployment
- **Database**: Managed PostgreSQL with automated backups
- **Security**: HTTPS, encrypted file storage, HIPAA-compliant data handling
- **Monitoring**: Application performance tracking and error reporting
- **Integration**: Webhook support for external system notifications

## Database Schema (Enhanced)

### Core Tables
```sql
-- Housing complexes/programs
complexes (id, name, config_json, created_at, updated_at)

-- Workflow stages (configurable per complex)
stages (
  id, complex_id, name, order, typical_days, max_days,
  responsible_party, config_json, created_at, updated_at
)

-- Applicants and their current status
applicants (
  id, complex_id, current_stage_id, name, email, phone, 
  case_manager, property_manager, unit_number,
  referral_date, created_at, stage_entered_at, updated_at
)

-- Stage transitions with bidirectional tracking
stage_transitions (
  id, applicant_id, from_stage_id, to_stage_id, 
  direction ('forward'|'backward'|'lateral'),
  transition_reason, changed_by, timestamp, 
  days_in_previous_stage, auto_generated
)

-- Contextual notes system
stage_notes (
  id, applicant_id, stage_id, note_type, category,
  content, created_by, created_at, is_system_generated,
  related_transition_id
)

-- Document management with reuse tracking
documents (
  id, applicant_id, document_type, file_path, 
  original_stage_id, reused_for_stages[], 
  uploaded_by, uploaded_at, verified_at, verified_by
)

-- Email communications log
email_log (
  id, applicant_id, stage_id, template_id, recipients,
  subject, sent_at, sent_by, delivery_status, 
  microsoft_graph_id
)

-- Process analytics and insights
process_metrics (
  id, applicant_id, stage_id, days_in_stage, 
  expected_days, variance, bottleneck_indicators,
  calculated_at
)

-- AI-generated summaries
ai_summaries (
  id, applicant_id, summary_type, content, 
  generated_at, model_version, confidence_score
)
```

### New Analytics Tables
```sql
-- Stage performance tracking
stage_performance (
  id, stage_id, period_start, period_end,
  avg_days, median_days, success_rate,
  common_delays[], bounce_back_rate
)

-- Bottleneck identification
process_bottlenecks (
  id, stage_id, bottleneck_type, frequency,
  avg_delay_days, common_reasons[], 
  suggested_improvements, identified_at
)

-- Stakeholder activity tracking
user_activity (
  id, user_id, applicant_id, action_type,
  stage_id, timestamp, duration_minutes
)
```

## User Roles & Permissions

### Primary Stakeholders
- **Admin** (Kody): Full system configuration, analytics access, AI summary management
- **Property Manager**: Manage applicants for their properties, send referrals, update tracking
- **Case Manager** (IHI/JOIN): Support assigned applicants, upload documents, monitor progress  
- **JOHS Staff**: View referral pipeline, track placement success rates
- **Applicant**: Self-service portal with status visibility and document upload

### Permission Matrix
| Feature | Admin | Prop Mgr | Case Mgr | JOHS | Applicant |
|---------|-------|----------|----------|------|-----------|
| View All Applicants | ✅ | Property Only | Assigned Only | All | Own Only |
| Move Between Stages | ✅ | ✅ | Limited | ❌ | ❌ |
| Add Contextual Notes | ✅ | ✅ | ✅ | ✅ | ❌ |
| Access Analytics | ✅ | Property Only | Assigned Only | Summary Only | ❌ |
| Configure Workflows | ✅ | ❌ | ❌ | ❌ | ❌ |
| AI Summaries | ✅ | ✅ | ✅ | ✅ | Own Only |

## Enhanced Features

### 1. Intelligent Kanban Board
- **Bidirectional Workflow**: 11 PSH-specific stages with forward/backward movement tracking
- **Smart Applicant Cards**: Name, days in stage, variance from expected timeline, document completion status
- **Contextual Drag & Drop**: Moving cards triggers stage-specific note prompts explaining transitions
- **Advanced Color Coding**: Green (on track), Yellow (approaching deadline), Red (overdue), Purple (bounced back)
- **Multi-Dimensional Filtering**: By responsible party, timeline variance, document status, bounce-back history

### 2. Stage-Specific Contextual Notes System
- **Smart Prompts**: Moving between stages triggers relevant questions ("Why was this returned?", "What caused the delay?")
- **Structured Data Capture**: Notes feel natural but capture categorized, searchable information
- **Bidirectional Context**: Different prompts for forward movement vs. bounce-backs
- **Auto-Classification**: System categorizes notes by type (documentation, applicant response, system delay, external factor)
- **Stakeholder Visibility**: Notes visible to appropriate parties based on stage and role

### 3. Process Analytics & Timeline Intelligence
- **Individual Process Visualization**: "Timelapse" view showing exactly how long each applicant spent in each stage
- **Bottleneck Identification**: Heat maps showing where delays most commonly occur
- **Comparative Analytics**: Compare individual cases to averages, identify outliers
- **Predictive Timelines**: Estimate completion dates based on current stage and historical data
- **Bounce-Back Analysis**: Track common reasons for backward movement and their resolution times

### 4. Document Intelligence System
- **Stage-Aware Uploads**: System knows which documents are needed at each stage
- **Reuse Optimization**: Tax Credit documents automatically available for HF Intake Packet
- **Smart Checklists**: Dynamic requirements based on family composition (birth certificates for children, IDs for adults 18+)
- **Verification Tracking**: Mark documents as reviewed/approved with timestamp and reviewer
- **Missing Document Alerts**: Proactive notifications when deadlines approach

### 5. Microsoft Graph Email Integration
- **Automated Stage Notifications**: Email appropriate stakeholders when applicants move between stages
- **Template Engine**: Stage-specific email templates with applicant information auto-fill
- **Communication Logging**: All emails tracked and linked to applicant records
- **Stakeholder Routing**: Different email lists for PSH vs HP units, different stages
- **Escalation Alerts**: Automatic notifications when timelines exceed thresholds

### 6. Multi-Stakeholder Dashboards
- **Property Manager View**: Focus on units available, referral requests, compliance deadlines
- **Case Manager View**: Assigned applicants, document needs, upcoming deadlines
- **JOHS Dashboard**: Referral pipeline, placement success rates, average timelines
- **Admin Analytics**: System-wide performance, bottleneck identification, process optimization insights

### 7. Claude AI Integration
- **Automated Process Summaries**: Generate comprehensive reports for completed applications
- **Pattern Recognition**: Identify common delay patterns and suggest improvements
- **Stakeholder-Specific Insights**: Tailored recommendations for different user types
- **Predictive Analysis**: Forecast potential issues based on current application patterns
- **Process Optimization Suggestions**: AI-driven recommendations for workflow improvements

## Current Implementation Status (October 6, 2025)

### ✅ **COMPLETED FEATURES**
The PSH Tracking Platform has evolved significantly beyond the original technical plan, with many Phase 3-4 features already implemented:

#### **Core Platform (Phase 1)**
- ✅ **Intelligent Kanban Board**: 11 PSH-specific stages with drag-and-drop functionality
- ✅ **Bidirectional Tracking**: Complete stage movement history with contextual notes
- ✅ **Time-Sensitive Tracking**: Configurable stage time limits with expiration date display
- ✅ **Editable Timelines**: Click-to-edit expiration dates with automatic recalculation
- ✅ **Privacy Compliance**: Initials-only system for enhanced data protection
- ✅ **Modal UI System**: Professional modal overlays for forms and document management

#### **Process Intelligence (Phase 2)**
- ✅ **Document Management**: Interactive document tracking with real-time status updates
- ✅ **Missing Documentation Modal**: Clickable status changes with save functionality
- ✅ **Enhanced Data Persistence**: Robust localStorage with validation and error handling
- ✅ **Action Items System**: Checkbox-based task management with automatic process logging
- ✅ **Dashboard Analytics**: Real-time statistics and active action items monitoring

#### **Advanced Features (Phase 3+)**
- ✅ **Professional UI/UX**: Modern, responsive design with color-coded status indicators
- ✅ **Data Export/Import**: Complete backup and restore functionality
- ✅ **Stage Information System**: Comprehensive process documentation and training materials
- ✅ **Email Template System**: Pre-built templates with variable substitution
- ✅ **County Integration**: HMIS number tracking for database connectivity

### 🚀 **PRODUCTION READY**
The platform is currently **production-ready** and being used for real PSH application tracking. All core functionality is implemented and tested, with robust error handling and data persistence.

### 📋 **REMAINING PHASES**
- **Phase 3**: Advanced analytics and AI integration (timeline visualization, bottleneck analysis)
- **Phase 4**: Multi-stakeholder platform with authentication and Microsoft Graph integration
- **Phase 5**: Advanced intelligence and scaling features

## Development Phases

### Phase 1: Enhanced Kanban Foundation (3-4 weeks) ✅ COMPLETED
- [x] Intelligent Kanban board with 11 PSH-specific stages
- [x] Bidirectional stage movement with transition tracking
- [x] Basic contextual note prompts for stage movements
- [x] Applicant CRUD with enhanced data fields (case manager, property manager, unit)
- [x] Stage transition history and timeline tracking
- [x] Time-sensitive tracking with configurable stage limits
- [x] Editable expiration dates with color-coded status indicators
- [x] Privacy-compliant initials-only system
- [x] Modal-based UI for forms and document management
- [ ] User authentication with role-based permissions (deferred for Phase 4)

### Phase 2: Contextual Intelligence (3-4 weeks) ✅ COMPLETED
- [x] Stage-specific note prompt system
- [x] Structured data capture from natural note-taking
- [x] Document upload with stage-aware requirements
- [x] Basic timeline analytics (days in stage, variance tracking)
- [x] Interactive document management with real-time status updates
- [x] Missing documentation modal with clickable status changes
- [x] Enhanced data persistence with robust validation
- [x] Simple process visualization (individual applicant timeline)
- [ ] Email notification foundation (Microsoft Graph setup) (deferred for Phase 4)

### Phase 3: Process Analytics & Insights (4-5 weeks)
- [ ] Advanced timeline visualization ("timelapse" view)
- [ ] Bottleneck identification and heat mapping
- [ ] Bounce-back analysis and pattern recognition
- [ ] Comparative analytics (individual vs. averages)
- [ ] Predictive timeline estimation
- [ ] Data export capabilities (CSV, Excel, PDF reports)
- [ ] Claude AI integration for automated summaries

### Phase 4: Multi-Stakeholder Platform (3-4 weeks)
- [ ] Stakeholder-specific dashboards (Property Manager, Case Manager, JOHS, Admin)
- [ ] Microsoft Graph email automation with template engine
- [ ] Advanced document intelligence (reuse optimization, smart checklists)
- [ ] Client-facing applicant portal with status visibility
- [ ] Real-time notifications and escalation alerts
- [ ] Process optimization suggestions from AI analysis

### Phase 5: Advanced Intelligence & Scaling (2-3 weeks)
- [ ] Machine learning for delay prediction and bottleneck forecasting
- [ ] Advanced AI insights and process improvement recommendations
- [ ] External system integration (webhooks, API access)
- [ ] Performance optimization for high-volume usage
- [ ] Comprehensive security audit and HIPAA compliance review
- [ ] Training materials and documentation for all stakeholders

### Continuous: Data Collection & Optimization
- [ ] Ongoing process metrics collection and analysis
- [ ] Regular AI model updates based on new data patterns
- [ ] Stakeholder feedback integration and UI/UX improvements
- [ ] Process refinement based on real-world usage analytics

## Security Considerations
- **Data Encryption**: All PII encrypted at rest and in transit
- **Access Control**: Role-based permissions with audit logging
- **HIPAA Compliance**: Secure handling of sensitive applicant information
- **File Security**: Virus scanning, file type restrictions
- **Session Management**: Secure authentication with session timeouts

## Testing Strategy
- **Unit Tests**: Backend API endpoints and business logic
- **Integration Tests**: Database operations and external services
- **E2E Tests**: Critical user workflows (add applicant, move stages)
- **User Testing**: Stakeholder feedback sessions during development

## Deployment Strategy
- **Staging Environment**: Mirror production for testing
- **Blue-Green Deployment**: Zero-downtime updates
- **Database Migrations**: Versioned schema changes
- **Monitoring**: Application performance and error tracking

## Success Metrics

### Process Improvement
- **Time Reduction**: 20-30% decrease in average application completion time
- **Bottleneck Elimination**: Identify and resolve top 3 process bottlenecks within 6 months
- **Bounce-Back Reduction**: 40% reduction in applications requiring rework or returned documents
- **Predictability**: 80% accuracy in timeline estimation for new applications

### Stakeholder Engagement
- **User Adoption**: 90%+ active usage by all stakeholder groups within 3 months
- **Data Quality**: 95% of stage transitions include contextual notes
- **Communication Efficiency**: 50% reduction in email chains and phone calls for status updates
- **Applicant Satisfaction**: Measurable improvement in applicant experience through portal usage

### System Intelligence
- **Process Insights**: Generate actionable process improvement recommendations monthly
- **Pattern Recognition**: Identify seasonal patterns, common delay causes, and optimization opportunities
- **Automation Success**: 80% of stage notifications sent automatically with relevant stakeholder routing
- **Data Export**: Regular reporting to stakeholders for compliance and process improvement

## Implementation Roadmap

### Immediate Next Steps (Week 1-2)
1. **Environment Setup**: Configure development environment with React, PostgreSQL, Microsoft Graph
2. **Stage Mapping**: Finalize the 11 PSH stages with accurate timelines and responsible parties
3. **Stakeholder Interviews**: Gather specific requirements from Property Managers, Case Managers, JOHS staff
4. **UI/UX Design**: Create wireframes for enhanced Kanban board with contextual note prompts

### Short-term Goals (Month 1-2)
1. **Phase 1 Development**: Build enhanced Kanban foundation with bidirectional tracking
2. **Microsoft Graph Integration**: Set up Outlook authentication and basic email automation
3. **User Testing**: Deploy beta version for core stakeholders to test and provide feedback
4. **Data Migration**: Plan migration strategy from existing Google Sheets tracking

### Medium-term Vision (Month 3-6)
1. **Full Feature Deployment**: Complete Phases 2-3 with analytics and AI integration
2. **Stakeholder Training**: Comprehensive onboarding for all user types
3. **Process Optimization**: Use initial data to identify and address bottlenecks
4. **Expansion Planning**: Prepare for additional housing complexes and program types

### Long-term Goals (6+ Months)
1. **Predictive Intelligence**: Advanced AI for forecasting delays and optimizing resource allocation
2. **Regional Scaling**: Expand to other housing authorities and coordinated access systems
3. **Policy Impact**: Use data insights to inform housing policy and process improvements
4. **Integration Ecosystem**: Connect with other housing services and case management systems

---
*Last Updated: October 6, 2025*
*Document Owner: Kody Barnett*
*Project Vision: Transform PSH application tracking from reactive management to proactive process intelligence*
*Current Status: Production-ready platform with advanced time-sensitive tracking and document management*