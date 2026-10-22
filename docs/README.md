\# Tutedude AWS Assignment — Pratheesh Babu



\## Project Overview



This project demonstrates deploying a Flask backend and an Express.js frontend using AWS infrastructure and Docker technologies.



\## Technologies



\- AWS EC2

\- Ubuntu Server 24.04 LTS

\- Python and Flask

\- Gunicorn

\- Node.js and Express.js

\- Docker and Docker Compose

\- Amazon ECR and ECS (planned deployment stage)



\## Deployment Progress



\### Deployment 1: Single EC2 Instance — Completed



\- EC2 instance: `Tutedude-AWS-Single-EC2`

\- Region: Mumbai (`ap-south-1`)

\- Operating system: Ubuntu Server 24.04 LTS

\- Instance type: `t2.micro`

\- Frontend: Express.js on port `3000`

\- Backend: Flask with Gunicorn on internal address `127.0.0.1:5000`

\- Process management: `systemd`

\- Frontend URL: http://15.206.203.33:3000



Both application services are configured to start automatically when the EC2 instance boots.



\### Deployment 2: Separate EC2 Instances



Status: Pending.



\### Deployment 3: Docker with ECR/ECS/VPC



Status: Pending.



\## Verification



\- Flask backend health endpoint: `/health`

\- Express frontend health endpoint: `/health`

\- Frontend-to-backend integration: Passed

\- Public browser test: Passed

\- Automatic service startup configuration: Completed



\## Screenshots



Deployment evidence is being collected in the `screenshots` folder.



\## Repository



GitHub: https://github.com/pratheeshbabus/AWS\_PratheeshBabu



\## Notes



The public IPv4 address may change if the EC2 instance is stopped and started. Update the frontend URL if the address changes. Verify AWS charges and remove resources when they are no longer needed.



