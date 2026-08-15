
# Network Config Manager Dashboard 🚀

## A full-stack self-service portal for network device management demonstrating Angular, MuleSoft API integration patterns, and OpenShift deployment with Terraform IaC.

## Status Angular Python FastAPI OpenShift Terraform License
## 📋 Table of Contents

    Overview
    Features
    Architecture
    Tech Stack
    Project Structure
    Getting Started
    API Documentation
    CI/CD Pipeline
    Deployment
    Screenshots
    Testing
    Contributing
    License

Overview

This project demonstrates enterprise-grade network automation tooling built with modern web technologies and cloud-native architecture. It serves as a proof-of-concept self-service portal where IT engineers can:

    View all network devices with real-time status monitoring
    Submit configuration changes through a change request workflow
    Track API health and performance metrics
    Manage device inventory through an intuitive Angular dashboard

Why This Matters

This project directly addresses requirements from the Federal Reserve Bank of Richmond Senior Network Automation Engineer position:
Job Requirement	Implementation Here
Angular UI development	Full Angular 17+ Material dashboard with RxJS state management
MuleSoft API Gateway	Mock gateway demonstrating API-led connectivity patterns
OpenShift/Kubernetes	Docker containers deployed to OpenShift with HPA autoscaling
Terraform IaC	Complete AWS infrastructure provisioning
CI/CD pipelines	GitLab CI with automated testing and deployment
Features
<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33 (3)" src="https://github.com/user-attachments/assets/7028b3bd-68df-461f-acca-a176c09b7c55" />

<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33 (2)" src="https://github.com/user-attachments/assets/1f74364f-2571-483e-968b-f23617410cfb" />

<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33" src="https://github.com/user-attachments/assets/61044731-a825-4a4c-ba5e-b91e69d0bf41" />






🖥️ Frontend (Angular)

    Real-time device status dashboard with color-coded indicators
    Inline YAML/JSON configuration editor with validation
    Change request submission with approval workflow tracking
    WebSocket connections for live status updates
    Role-based access control with route guards
    Responsive design for mobile/desktop views

🔌 Backend (Mock MuleSoft Gateway)

    OAuth2 token validation middleware
    Rate limiting policy enforcement (100 requests/minute)
    RAML API specification compliance
    DataWeave-style transformation engine
    ServiceNow ticket integration simulation
    Error handling and logging infrastructure

☁️ Infrastructure (AWS + OpenShift)

    VPC with public/private subnet isolation
    RDS PostgreSQL for legacy database simulation
    S3 + CloudFront for frontend CDN delivery
    Horizontal Pod Autoscaler (CPU-based scaling)
    Secrets management via OpenShift Secret objects
    CloudWatch logging and monitoring

Architecture
┌─────────────────────────────────────────────────────────────┐
│                      FULL STACK DEMO                         │
│                                                              │
│   ┌───────────┐     ┌─────────────┐     ┌─────────────────┐  │
│   │  Angular  │────▶│  MuleSoft   │────▶│  ServiceNow     │  │
│   │ Dashboard │     │ API Gateway │     │ (Mock/Real)     │  │
│   └───────────┘     └──────┬──────┘     └─────────────────┘  │
│                            │                                  │
│                     ┌──────┴──────┐    ┌─────────────────┐    │
│                     │   Python    │───▶│ Legacy DB       │    │
│                     │  FastAPI    │    │ (PostgreSQL)    │    │
│                     └─────────────┘    └─────────────────┘    │
│                                                                │
│   Deploy: Red Hat OpenShift (Docker containers)                │
│   CI/CD:  GitLab CI with Terraform IaC                         │
│   Monitor: CloudWatch + Prometheus metrics                     │
└─────────────────────────────────────────────────────────────┘
Tech Stack
Frontend
Technology	Version	Purpose
Angular	17+	Reactive web framework
Angular Material	17+	UI component library
RxJS	7+	Reactive state management
Tailwind CSS	3+	Utility-first styling
TypeScript	5+	Type-safe JavaScript
Backend
Technology	Version	Purpose
Python	3.11+	Runtime environment
FastAPI	0.100+	High-performance API framework
Pydantic	2+	Data validation
Uvicorn	0.23+	ASGI server
pytest	7+	API testing
Infrastructure
Technology	Purpose
Docker	Containerization
Red Hat OpenShift	Kubernetes orchestration
Terraform	Infrastructure as Code
AWS	Cloud provider (VPC, RDS, S3, CloudFront)
GitLab CI	CI/CD pipeline orchestration
Project Structure
network-automation-portfolio/
├── README.md                          # This file
├── frontend/                          # Angular dashboard
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/            # Reusable UI components
│   │   │   │   ├── device-list/       # Network device table
│   │   │   │   ├── config-editor/     # YAML/JSON config inline edit
│   │   │   │   ├── api-status/        # Health check dashboard
│   │   │   │   └── change-request/    # Submit change forms
│   │   │   ├── services/              # HTTP & WebSocket services
│   │   │   │   ├── device-api.service.ts
│   │   │   │   ├── auth-guard.service.ts
│   │   │   │   └── websocket.service.ts
│   │   │   ├── models/
│   │   │   │   └── device.model.ts    # TypeScript interfaces
│   │   │   ├── app-routing.module.ts  # Lazy-loaded routes
│   │   │   └── app.component.ts
│   │   ├── assets/                    # Images & static files
│   │   └── environments/
│   │       └── environment.ts         # Environment variables
│   ├── angular.json
│   ├── package.json
│   ├── proxy.conf.json                # API proxy configuration
│   ├── Dockerfile                     # Multi-stage build
│   └── nginx.conf                     # Production server config
│
├── gateway/                           # MuleSoft mock (Python/FastAPI)
│   ├── mock_mulesoft_gateway.py       # Main application
│   ├── raml/
│   │   └── network-device-api.raml    # API specification
│   ├── tests/
│   │   ├── test_api.py               # API endpoint tests
│   │   └── test_rate_limit.py        # Rate limiting tests
│   ├── requirements.txt
│   └── Dockerfile
│
├── infrastructure/                    # Terraform IaC
│   ├── main.tf                        # Root module
│   ├── variables.tf                   # Input parameters
│   ├── outputs.tf                     # Output values
│   ├── vpc/                          # VPC sub-module
│   ├── rds/                          # RDS sub-module
│   └── s3-cloudfront/                # CDN sub-module
│
├── openshift/                         # Kubernetes manifests
│   ├── deployment.yaml                # App deployments
│   ├── service.yaml                   # Cluster services
│   ├── route.yaml                     # External routing
│   └── hpa.yaml                       # Horizontal pod autoscaling
│
├── docs/
│   ├── architecture-diagram.png       # Visual architecture
│   ├── api-flow-diagram.png           # Request flow visualization
│   └── screenshots/                   # UI screenshots
│       ├── dashboard-view.png
│       ├── config-editor.png
│       └── change-request-form.png
│
└── .gitlab-ci.yml                     # CI/CD pipeline definition
Getting Started
Prerequisites
# Required software
Node.js 18+             (for Angular development)
Python 3.11+           (for gateway development)
Docker 20+             (for containerization)
Terraform 1.5+         (for IaC)
oc CLI                  (for OpenShift deployment)
Installation
1. Clone the Repository
git clone https://github.com/pclumson/network-automation-portfolio.git
cd network-automation-portfolio
2. Setup Frontend (Angular)
cd frontend

# Install dependencies
npm ci

# Start development server (with API proxy to backend)
ng serve --proxy-config proxy.conf.json

# Access at http://localhost:4200
3. Setup Backend (Gateway)
cd gateway

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Run API server
uvicorn mock_mulesoft_gateway:app --reload --port 8081

# Access at http://localhost:8081
4. Test the API
# Get devices (requires valid token)
curl -H "Authorization: Bearer valid-demo-token" \
     http://localhost:8081/api/devices

# Update device configuration
curl -X PUT -H "Authorization: Bearer valid-demo-token" \
     -H "Content-Type: application/json" \
     -d '{"configuration": {"vlan": 100}, "reason": "Network optimization", "priority": "high"}' \
     http://localhost:8081/api/devices/dev-001/config
API Documentation
Base URL
Production: https://api.frb.example.com/v1
Development: http://localhost:8081
Authentication

All endpoints require OAuth2 bearer token authentication.
Authorization: Bearer <token>

Valid demo tokens:
valid-demo-token
admin-demo-token
Endpoints
GET /api/devices

Retrieve all network devices.

Response: 200 OK
[
  {
    "id": "dev-001",
    "name": "Core-Router-01",
    "ipAddress": "10.0.1.1",
    "manufacturer": "Cisco",
    "model": "ISR4331",
    "status": "online",
    "location": "Datacenter A"
  }
]

Rate Limit Headers:
X-RateLimit-Limit: 100
X-RateLimit-Remaining: 99
PUT /api/devices/{deviceId}/config

Submit a device configuration change request.

Request Body:
{
  "configuration": {
    "vlan": 100,
    "mtu": 9000
  },
  "reason": "Network optimization",
  "priority": "high"
}

Response: 202 Accepted
{
  "status": "submitted",
  "ticketId": "CHG123456",
  "timestamp": "2026-08-15T22:17:38Z"
}
Error Responses
Status Code	Description
400	Bad Request - Invalid payload format
401	Unauthorized - Missing or invalid token
404	Not Found - Device ID does not exist
429	Too Many Requests - Rate limit exceeded
500	Internal Server Error - Gateway failure
CI/CD Pipeline

Automated workflows on every push to main branch:
stages:
  - test        → Run unit tests for both projects
  - build       → Build Docker images
  - terraform   → Plan & apply infrastructure changes
  - deploy      → Roll out to OpenShift cluster
Pipeline Stages
graph LR
    A[Push to main] --> B[test_frontend]
    A --> C[test_gateway]
    B --> D[build_images]
    C --> D
    D --> E[terraform_plan]
    E --> F{Approve?}
    F -->|Yes| G[terraform_apply]
    F -->|No| H[Cancel]
    G --> I[deploy_openshift]
Manual Steps
# Trigger pipeline manually via GitLab UI
# Or use CLI:
glab pipeline create --branch main

# Check pipeline status:
gitlab-ci status

# View logs:
docker logs ${CI_REGISTRY}/frontend:${CI_COMMIT_SHA}
Deployment
Option 1: Local Development (Docker Compose)
# Start all services locally
docker-compose up --build

# Access services:
# Frontend: http://localhost:4200
# Gateway:  http://localhost:8081
# Database: localhost:5432
Option 2: OpenShift Production Deployment
# Login to OpenShift cluster
oc login --server=${OPENSHIFT_SERVER} --token=${OPENSHIFT_TOKEN}

# Create new project
oc new-project network-automation-demo

# Deploy applications
oc apply -f openshift/deployment.yaml
oc apply -f openshift/route.yaml
oc apply -f openshift/hpa.yaml

# Expose services externally
oc expose svc/frontend
oc expose svc/gateway

# Verify rollout
oc get pods
oc get routes

# Monitor logs
oc logs -f deployment/frontend
oc logs -f deployment/gateway
Option 3: AWS Infrastructure (Terraform)
# Configure Terraform
export TF_VAR_aws_region="us-east-1"
export TF_VAR_db_username="admin"
export TF_VAR_db_password="<secure-password>"

# Initialize
cd infrastructure
terraform init

# Plan infrastructure changes
terraform plan -out=tfplan

# Review plan output
terraform show tfplan

# Apply changes (manual approval required)
terraform apply tfplan

# Outputs after apply:
# - frontend_url = https://network-automation-frontend-demo.s3.amazonaws.com
# - gateway_endpoint = https://api.network-automation.internal
Screenshots
<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33 (3)" src="https://github.com/user-attachments/assets/55704fe7-497e-4bb7-9ccf-19375f2f5ca1" />

Dashboard View
<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33 (2)" src="https://github.com/user-attachments/assets/a44bf155-53a5-4339-a4df-e9c83df69e23" />

Dashboard
<img width="1280" height="720" alt="Lumo generated 2026-08-15 17 33" src="https://github.com/user-attachments/assets/7495103d-b736-46f4-a840-5109facbc468" />

Real-time device status with online/offline indicators
Configuration Editor

Config Editor

Inline YAML configuration editing with validation
Change Request Form

Change Request

Submit change requests with priority and reason fields
Testing
Frontend Tests
cd frontend

# Run unit tests
npm test -- --watch=false --browsers=ChromeHeadless

# Run linting
npm run lint

# Generate coverage report
npm run test -- --code-coverage
Backend Tests
cd gateway

# Run API tests
pytest tests/ -v --junitxml=test-results.xml

# Run with coverage
pytest --cov=mock_mulesoft_gateway --cov-report=html
Test Coverage Report
Name                               Stmts   Miss  Cover
------------------------------------------------------
mock_mulesoft_gateway.py           150     12    92%
test_api.py                         80      3    96%
test_rate_limit.py                  45      2    96%
------------------------------------------------------
TOTAL                              275     17    94%
Contributing

This is a demonstration portfolio project. Contributions are welcome!

    Fork the repository
    Create your feature branch (git checkout -b feature/amazing-feature)
    Commit your changes (git commit -m 'Add some amazing feature')
    Push to the branch (git push origin feature/amazing-feature)
    Open a Pull Request

Security Considerations

⚠️ Important: This project uses placeholder credentials and mock integrations for demonstration purposes only.

Before deploying to production:

    Replace all demo OAuth2 tokens with real identity providers (Keycloak, Auth0, etc.)
    Configure proper TLS/SSL certificates
    Implement secrets management (HashiCorp Vault, AWS Secrets Manager)
    Enable audit logging for all API calls
    Set up intrusion detection systems
    Regular security vulnerability scanning
    Compliance with FedRAMP/NIST guidelines (for government deployments)

Related Projects

    Smart Health Application - Healthcare data management
    DJ-APIs-Allauth - Django REST API framework
    Polars DataFrame Deduplication - Performance optimization

Contact

    Email: prince.eklu@proton.me
    LinkedIn: linkedin.com/in/prince-clumson-eklu-92a6b476
    GitHub: github.com/pclumson

License

MIT License - See LICENSE file for details.
<!-- PROJECT METADATA ═══════════════════════════ Repository: pclumson/network-automation-portfolio Last Updated: August 15, 2026 Maintainer: Prince Clumson-Eklu Star this repo if it helps your job search! ⭐ -->
