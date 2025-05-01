# Cloud Computing PA2: Wine Quality Prediction

** Prerequisites**
- AWS account with EC2 access
- Docker installed (for local testing)
- Files required:
  - `cloud_computing_pa2` (application JAR)
  - `TrainingDataset.csv`
  - `ValidationDataset.csv`
  - `TestDataset.csv`

 AWS EMR Setup
1. **Upload to S3
2.Create EMR Cluster:
Select "Spark" application
4 EC2 instances (1 master + 3 workers)
IAM role with S3 access

**Model Training**
To train the model:
Navigate to the EMR cluster dashboard
Select "Steps" and click "Add step"
Choose "Spark Application"
Configure the step:
Provide a meaningful name
Select your JAR file
Add --class com.example.Train to spark-submit options
Click "Add step" to begin training
The training process will create and save the best performing model to S3.

**Model Testing**
To test the trained model:
Navigate to the EMR cluster dashboard
Select "Steps" and click "Add step"
Choose "Spark Application"
Configure the step:
Provide a meaningful name
Select your JAR file
Add --class com.example.Test to spark-submit options
Click "Add step" to begin testing


**Docker Deployment 

### 1. Build Docker Image
```bash
docker build -t cloud_computing_pa2.

docker run \
  -v $(pwd)/model:/model \
  -v $(pwd)/data:/data \
  cloud_computing_pa2 \
  spark-submit \
  --class com.example.Test \
  /app.jar \
  /model \
  /data/TestDataset.csv

# Login (use your Docker Hub credentials)
docker login

# Tag and push
docker tag wine-prediction:latest yourusername/cloud_computing_pa2
docker push yourusername/cloud_computing_pa2

docker pull yourusername/cloud_computing_pa2
docker run -v $(pwd)/test_data:/data yourusername/cloud_computing_pa2
