## AWS Infrastructure Setup

- Create two Ubuntu 26.04 LTS EC2 instances in the same VPC:
  - One for the MERN frontend (React).
  - One for the MERN backend (Node.js/Express).
- Use `t3.micro`.
- Configure security groups to allow inbound:
  - SSH (port 22) from your IP.
  - HTTP (port 80) for NGINX.
  - Application ports (e.g., 3000 for frontend, 3001 for backend) for internal testing.
## MERN Application Deployment

### Backend (Express + MongoDB)

1. SSH into the backend EC2 instance.
2. Install Node.js and npm:
   ```bash
   sudo apt update
   sudo apt install -y nodejs npm
   ```
3. Clone the backend repository:
   ```bash
   git clone https://github.com/Rishav-Mukhopadhyay/aws_assignment_HeroVired.git
   cd aws_assignment_HeroVired/backend
   ```
4. Install dependencies and start the server:
   ```bash
   npm install
   node index.js
   ```
### Frontend (React)

1. SSH into the frontend EC2 instance.
2. Install Node.js and npm:
   ```bash
   sudo apt update
   sudo apt install -y nodejs npm
   ```
3. Clone the frontend repository:
   ```bash
   git clone https://github.com/Rishav-Mukhopadhyay/aws_assignment_HeroVired.git
   cd aws_assignment_HeroVired/frontend
   ```
4. Configure API base URL to point to the backend (later via NGINX/ALB, e.g. `/api`).
5. Install dependencies and start the dev server:
   ```bash
   npm install
   npm start
   ```
6. For production, build the React app and serve it through NGINX or a dedicated Node server:
   ```bash
   npm run build
   ```
## NGINX Reverse Proxy Configuration

Install and configure NGINX on a chosen entry-point instance (often the frontend EC2):

1. Install NGINX:
   ```bash
   sudo apt update
   sudo apt install -y nginx
   ```
2. Edit the default site configuration:
   ```bash
   sudo nano /etc/nginx/sites-available/default
   ```
3. Example configuration:
   ```nginx
   server {
       listen 80;

       location /api {
           proxy_pass http://<BACKEND_PRIVATE_IP>:<BACKEND_PORT>;
       }

       location / {
           proxy_pass http://<FRONTEND_PRIVATE_IP>:3000;
       }
   }
   ```
4. Test and reload:
   ```bash
   sudo nginx -t
   sudo systemctl reload nginx
   ```