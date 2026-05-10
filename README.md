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
4. Add environment varialbles
   ```bash
   nano .env
   ```
   ```bash
   MONGO_URI='mongodb+srv://rishav1994sonai_db_user:eud40m7e2Ygheflj@travelmemory.x5yt4i8.mongodb.net/?appName=TravelMemory'
   PORT=3001
   ```
5. Install dependencies and start the server:
   ```bash
   npm install
   node index.js
   ```