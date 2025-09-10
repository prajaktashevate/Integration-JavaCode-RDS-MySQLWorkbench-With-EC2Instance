📌 Project Objective :-
=
The main objective of this project is to deploy a Java application on an EC2 instance and integrate it with an AWS RDS MySQL database. The application interacts with the database (CRUD operations), while MySQL Workbench is used for remote database management and monitoring. This setup demonstrates a scalable, secure, and cloud-based architecture for hosting enterprise applications.

📌 Project Description:-
=
A Java application is deployed on an EC2 instance (Linux/Windows) to act as the application server.

The application connects to an RDS MySQL database for data storage and retrieval.

MySQL Workbench is used locally by developers/DBAs to manage, monitor, and query the RDS database securely.

AWS Security Groups are configured to allow communication between EC2 and RDS, and between MySQL Workbench and RDS.

This setup simulates a real-world cloud deployment where applications run on compute nodes (EC2) while leveraging managed database services (RDS).

📌 Architecture Flow :-
=
Step-by-step flow:

1.User/Application Request → End-user interacts with the Java application hosted on EC2.

2.EC2 Instance (App Layer) → Java code executes logic and connects to the RDS MySQL endpoint.

3.RDS MySQL (DB Layer) → Handles queries (Insert, Select, Update, Delete) and sends responses back to EC2.

4.MySQL Workbench (from developer system) → Connects to RDS for schema design, monitoring, and query execution.

5.Data Flow → MySQL RDS ↔ EC2 Java Code ↔ MySQL Workbench.
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/084f5ae2-84d4-437d-9f99-fa4b2eb36fec" />


📌 Benefits of This Setup:-
=

✅ Scalability – EC2 instances can be scaled up/down, and RDS supports Multi-AZ & Read Replicas for scaling databases.

✅ Separation of Concerns – Application (EC2) and Database (RDS) are independent, improving reliability and manageability.

✅ High Availability – RDS provides automatic backups, snapshots, and failover for business continuity.

✅ Security – Controlled access via Security Groups, IAM roles, and encryption.

✅ Ease of Management – MySQL Workbench allows developers to manage RDS without logging into AWS console.

✅ Real-world Cloud Simulation – Mirrors enterprise setups where apps and DBs are hosted separately.

✅ Cost Optimization – Pay-as-you-go model with options for reserved instances and database scaling.


