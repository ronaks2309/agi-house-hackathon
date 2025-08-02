1. Project Overview
Objective: Create a proof-of-concept application that identifies people from photos and generates conversational insights based on their professional profiles.

High-Level Flow:

User uploads photo via web interface
System detects/identifies person in photo
Matches person to database profile
Generates conversational data using LLM integration
Returns personalized conversation starters/insights

```
graph TD
    A[Frontend Upload] --> B[Supabase Storage]
    B --> C[n8n Webhook]
    C --> D[Face Detection API]
    D --> E[Face Recognition Service]
    E --> F[Supabase Profile Query]
    F --> G[LLM API]
    G --> H[Response to Frontend]
```

2. Functional Requirements
**2.1 Frontend Application**
Photo Upload Interface
Drag & drop photo upload
File format support: JPG, PNG, WEBP
Image preview before submission
Upload progress indicator
Error handling for invalid files
Results Display

Show identified person's profile information
Display generated conversational insights
Professional headshot from database
Contact information (if available)

**2.2 Person Detection & Recognition**
Face Detection: Identify faces in uploaded photos
Face Recognition: Match detected faces to database profiles
Multi-person Handling: Handle photos with multiple people
Confidence Scoring: Return match confidence levels

**2.3 Database Requirements (Supabase)**
Profiles Table
person_id (UUID, primary key)
full_name
linkedin_url
profile_image_url
job_title
company
location
bio/summary
skills (JSON array)
experience (JSON array)
education (JSON array)
face_encoding (for recognition)
created_at/updated_at

**2.4 n8n Workflow Integration**
Webhook Endpoint: Receive photo data from frontend
Image Processing: Call face detection/recognition service
Database Query: Search Supabase for matching profiles
LLM Integration: Generate conversational insights
Response Handling: Return structured data to frontend

**2.5 LLM Conversation Generation**
Input Processing: Use profile data as context
Conversation Starters: Generate relevant talking points
Professional Insights: Create business-relevant conversation topics
Personalization: Tailor responses based on shared connections/interests

3. Technical Requirements
3.1 Frontend Stack
React with TypeScript
Tailwind CSS for styling
File upload handling
HTTP client for API communication
3.2 Backend Services
Supabase: Database and authentication
n8n: Workflow automation and orchestration
Face Recognition Service: (Azure Face API, AWS Rekognition, or open-source alternative)
LLM Service: (OpenAI GPT, Claude, or local model)
3.3 Data Flow Architecture
Frontend → n8n Webhook → Face Recognition → Supabase Query → LLM Processing → Frontend Response

5. User Stories
As a User:
I want to upload a photo and quickly identify who is in it
I want to see relevant professional information about the identified person
I want conversation starters that help me connect professionally
I want the process to be fast and intuitive
As a System:
Process photos accurately and securely
Maintain up-to-date profile information
Generate relevant and helpful conversation insights
Handle errors gracefully with clear feedback

6. Success Criteria
MVP Success Metrics:
Accuracy: 80%+ face recognition accuracy
Speed: End-to-end processing under 30 seconds
User Experience: Intuitive interface with clear feedback
**Data Quality: Meaningful conversation insights generated**