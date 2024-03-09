# social-unite
Social Unite App

Focusing on a robust infrastructure plan for backend API services and a separate frontend application is crucial for ensuring scalability, maintainability, and security.


### 1. Backend API Services

The backend API services will be the backbone of your application, handling user management, authentication, and business logic. Here's a highlevel approach for each service:

#### a. User Signup
- **Technology Stack**: Consider using Node.js with Express for a lightweight, efficient backend, or FastAPI for Python ecosystem for its robustness.
- **Database**: PostgreSQL or MySQL. Both offers relational data integrity.
- **Features**: Collect necessary user information using form, validate it (frontend UI validations), and store it in the database. Implement CAPTCHA or similar mechanisms to prevent bot registrations.

#### b. Authentication
- **Technology**: JSON Web Tokens (JWT) for stateless authentication.
- **Flow**: Implement OAuth2.0 for secure authorization, especially if we plan to allow third-party logins (eg. GMail) in the future.
- **Security**: Ensure passwords are hashed using bcrypt or a similar library. Implement rate limiting and account lockout mechanisms to prevent brute force attacks.

#### c. User Signup Approval
- **Approach**: This can be automated based on criteria (e.g., email domain verification) or manually done by admins.
- **Tools**: Use an admin dashboard for manual approval. For automated approval, implement business logic in API to verify the criteria and approve the signup.

#### d. Service to Map Relationships Within Users
- **Functionality**: Service for mapping relationships within users focuses on actual family relationships, such as father, mother, children, and self and functionality to accurately represent and manage these relationships.
- **Implementation Approach**: 

#### Data Modeling

- **Database Choice**: For relational data like family trees, a relational database like PostgreSQL could be more suitable due to its ability to enforce data integrity and relationships through foreign keys. However, if we anticipate complex queries involving many-to-many relationships or expect to scale significantly, a graph database like Neo4j might be more efficient for querying interconnected data.
  
- **Schema Design**: Design database schema to include entities for `User` and `Relationship`. The `User` entity would store information about each person, while the `Relationship` entity would define the type of relationship (e.g., father, mother, child) and link between two `User` entities. 

    - For a graph database, nodes would represent users, and edges would represent relationships with properties defining the relationship type.
    - For a relational database, we might have a `Users` table and a `Relationships` table where `Relationships` has columns for `user_id`, `related_user_id`, and `relationship_type`.

#### API Design

- **Endpoints**: Create RESTful endpoints or GraphQL queries/mutations to manage users and their relationships. This could include:
    - Adding/updating/deleting users
    - Adding/updating/deleting relationships between users
    - Querying relationships (e.g., fetching all children of a user, finding siblings, etc.)

- **Business Logic**: Implement logic to handle:
    - Validating relationship types (to ensure they fit within defined family relationship model)
    - Preventing circular or invalid relationships (e.g., ensuring a user cannot be their own parent)
    - Handling complex family structures (e.g., step-relations, adoptions)

#### Security and Privacy

- **Access Control**: Ensure that users can only view or modify relationships for which they have permission. This might involve role-based access control (RBAC) or more granular permissions.
  
- **Data Protection**: Family data is sensitive. Implement strong encryption for data at rest and in transit, and consider additional privacy measures like anonymizing data where appropriate.


### 2. Frontend App

The frontend app should be user-friendly and responsive to cater to a wide range of devices.

- **User Interface**: Design an intuitive UI that allows users to easily add and visualize family relationships. Interactive family trees or diagrams can be very effective here.
- **Interactivity**: Use AJAX or WebSocket connections for a dynamic experience, allowing users to see updates in real-time as they add or modify relationships.
- **Privacy and Sharing**: Provide clear options for users to control who can see their family information. Consider features like private profiles or sharing permissions.
- **Technology Stack**: Consider using React.js or Vue.js or any other front end tech. Both are popular, supported by large communities, and can help you create a dynamic and responsive UI.
- **Separation**: Host frontend and backend separately to decouple the user interface from your API logic. This approach enhances security and allows independent scaling of each component.
- **Communication**: Ensure secure HTTPS communication between your frontend and backend. Use tokens for managing user sessions and making authenticated API requests.
- **Deployment**: Containerization with Docker and orchestration with Kubernetes for both frontend and backend services would be considered and implemented. This setup facilitates scaling, development, and deployment processes.

### General Recommendations

- **Infrastructure as Code (IaC)**: Use tools like Terraform or AWS CloudFormation to manage your infrastructure, allowing you to define and deploy resources through code. (Not required for initial setup)
- **Continuous Integration/Continuous Deployment (CI/CD)**: Set up pipelines using Jenkins, GitLab CI/CD, or GitHub Actions to automate testing and deployment.
- **Monitoring and Logging**: Implement monitoring and logging solutions like Prometheus, Grafana, and ELK Stack for real-time performance monitoring and log management.

Remember, the choices in technology and tools should align with your team's expertise, project requirements, and long-term maintenance capabilities. It's also vital to implement security best practices from the start, including regular code reviews, secure coding practices, and penetration testing.
