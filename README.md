# pythonapp-deployment
Deployment of the pythonapp to EKS Cluster

Steps to perform before executing the pythonapp deployment:
1. Install mysql and connect to the RDS DBInstance that has been created by https://github.com/Dhruval59/terraform-EKS-RDS<br>
```mysql -h <DB-endpoint> -u admin -p```
2. Perform Database operations:
```
CREATE DATABASE flaskapp;
USE flaskapp;
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100)
);
INSERT INTO users (name, email) VALUES ('Dhruval', 'dhruval@example.com');
SELECT * FROM users;
```
3. Create kubectl secrets: flask-db-secret
```
kubectl create secret generic flask-db-secret \
  --from-literal=DB_HOST=<DB-endpoint> \
  --from-literal=DB_USER=admin \
  --from-literal=DB_PASSWORD=##### \
  --from-literal=DB_NAME=flaskapp
```
4. Apply kubernetes deployment, services and HPA
```
kubectl apply -f pythonapp-deployment/
```
