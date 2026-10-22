\# Tutedude AWS Assignment — Deployment Documentation



\*\*Student:\*\* Pratheesh Babu  

\*\*Project:\*\* Flask Backend and Express Frontend on AWS  

\*\*GitHub Repository:\*\* https://github.com/pratheeshbabus/AWS\_PratheeshBabu



\---



\## 1. Deployment 1 — Single EC2 Instance



\### 1.1 Objective



Deploy a Flask backend and an Express.js frontend on a single Amazon EC2 instance. Configure both applications to run as background services and start automatically after a server reboot.



\### 1.2 AWS Infrastructure



| Property | Value |

|---|---|

| EC2 instance name | Tutedude-AWS-Single-EC2 |

| AWS Region | Mumbai (`ap-south-1`) |

| Operating system | Ubuntu Server 24.04 LTS |

| Instance type | `t2.micro` |

| Root storage | 8 GiB gp3 |

| Frontend port | TCP 3000 |

| Backend port | TCP 5000, bound to localhost only |

| Frontend URL | http://15.206.203.33:3000 |



\### 1.3 Application Architecture



The Express.js frontend receives browser requests on port 3000 and communicates with the Flask backend through `http://127.0.0.1:5000`.



The Flask backend is bound to localhost, so port 5000 does not need to be exposed publicly.



\### 1.4 Software Installation



The following commands were used to install the required software on Ubuntu:



```bash

sudo apt update

sudo apt install -y python3 python3-pip python3-venv

sudo apt install -y nodejs npm

```



The repository was cloned using:



```bash

git clone https://github.com/pratheeshbabus/AWS\_PratheeshBabu.git

```



The Python virtual environment and backend dependencies were prepared using:



```bash

cd \~/AWS\_PratheeshBabu/backend

python3 -m venv .venv

source .venv/bin/activate

python -m pip install -r requirements.txt

```



The frontend dependencies were installed using:



```bash

cd \~/AWS\_PratheeshBabu/frontend

npm install

```



\### 1.5 Application Configuration



\*\*Flask backend\*\*



\- Application framework: Flask

\- Production server: Gunicorn

\- Internal address: `127.0.0.1:5000`

\- Health endpoint: `/health`



\*\*Express frontend\*\*



\- Runtime: Node.js

\- Framework: Express.js

\- Listening port: `3000`

\- Backend URL: `http://127.0.0.1:5000`

\- Health endpoint: `/health`



\### 1.6 Automatic Service Management



Both applications were configured as Ubuntu `systemd` services.



Backend service file:



`/etc/systemd/system/tutedude-backend.service`



Frontend service file:



`/etc/systemd/system/tutedude-frontend.service`



The services were enabled and started using:



```bash

sudo systemctl daemon-reload

sudo systemctl enable --now tutedude-backend

sudo systemctl enable --now tutedude-frontend

```



Service status can be checked using:



```bash

sudo systemctl status tutedude-backend --no-pager

sudo systemctl status tutedude-frontend --no-pager

```



Both services were verified as `active (running)`.



\### 1.7 Testing and Verification



\*\*Test the Flask backend health endpoint:\*\*



```bash

curl http://127.0.0.1:5000/health

```



Expected response:



```json

{"status":"healthy"}

```



\*\*Test the Express frontend health endpoint:\*\*



```bash

curl http://127.0.0.1:3000/health

```



Expected response:



```json

{"status":"healthy","service":"Express Frontend"}

```



\*\*Verify frontend-to-backend integration:\*\*



```bash

curl -s http://127.0.0.1:3000/ | grep -E "Tutedude AWS Assignment|Flask Backend|Backend status|Frontend status"

```



The output confirmed that the frontend displayed the Flask backend and that both application statuses were `running`.



\*\*Public browser test:\*\*



The frontend was accessed successfully at:



http://15.206.203.33:3000



\### 1.8 Security Configuration



The EC2 security group was configured with:



\- TCP 22 (SSH): restricted to the authorized client IP address.

\- TCP 3000 (frontend): restricted to the authorized client IP address.

\- TCP 5000 (backend): not exposed publicly.



The private SSH key was kept outside the project repository.



\### 1.9 Screenshots



The following evidence has been captured or identified for the single-EC2 deployment:



1\. `AWS\_Single\_EC2\_Public\_Deployment.png` — successful public browser page.

2\. `AWS\_Single\_EC2\_Systemd\_Services.png` — backend and frontend service status.



Additional terminal verification screenshots can be added if available.



\### 1.10 Result



\*\*Status: Completed.\*\*



The Flask backend and Express frontend were successfully deployed on one EC2 instance. The applications communicated correctly, the public frontend was accessible from the authorized client, and both services were configured to start automatically after reboot.



\---



\## 2. Deployment 2 — Separate EC2 Instances



\*\*Status:\*\* Pending.



This section will be completed after deploying the Flask backend and Express frontend on separate EC2 instances and verifying their communication.



\## 3. Deployment 3 — Docker, ECR, ECS and VPC



\*\*Status:\*\* Pending.



This section will be completed after the container deployment and its verification.



\---



\## Project Repository



https://github.com/pratheeshbabus/AWS\_PratheeshBabu



\*\*Documentation note:\*\* Verify the public IP address and screenshot filenames before final submission. The EC2 public IP may change after a stop/start operation.



