###################################
system_vendor_budget_manager
###################################

====================================
system_vendor_budget_manager
====================================
| Responsible for accepting, transferring, and recording publishers' budgets.
| system_vendor_budget_manager provides the following functionalities:

- Management of the system vendor's LEVICA account
- Publisher registration
- LEVICA account verification and transaction logging
- Triggering the payment function to the Extractor
- Budget output

| It also accepts the following request APIs from publishers:

- Direct specification of budget amount (in Anima)
- Specification of the logic for calculating purchase budgets

System Architecture
====================

Each component is built using a serverless architecture based on AWS Lambda and utilizes the following tech stack:

- **Language**: Python 3.12  
- **Infrastructure**: AWS (Lambda, ECS, ECR, EventBridge, etc.)  
- **IaC**: Terraform  
- **Database**: PostgreSQL  
- **Container Technology**: Docker, ECS Fargate  
- **Migration**: Alembic  

| For access to related assets, please contact ARCANA Technical Support.
