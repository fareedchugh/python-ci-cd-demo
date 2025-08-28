# Python CI/CD Demo with Jenkins & Docker

## Steps:
1. Clone repo:
   ```bash
   git clone https://github.com/YOUR-USERNAME/python-ci-cd-demo.git
   cd python-ci-cd-demo
   ```

2. Run locally:
   ```bash
   pip install -r requirements.txt
   python app/main.py
   ```

   Visit: `http://localhost:5000`

3. Run tests:
   ```bash
   pytest --cov=app
   ```

4. Docker build & run:
   ```bash
   docker build -t myapp .
   docker run -d -p 5000:5000 myapp
   ```

5. Jenkins will:
   - Pull code from GitHub
   - Run tests + coverage
   - Run security scans
   - Build Docker image
   - Deploy container
