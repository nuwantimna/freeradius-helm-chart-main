# FreeRadius Helm Chart

## Configuration changes

To change configuration modify content of `freeradius` directory.

## Deployment

We use [helm](https://helm.sh/) to deploy freeradius on EKS.

## Building with CI (Recommended way)

1. Clone this repo and create a new branch:

```
git clone git@gitlab.com:dgtek.net/freeradius-helm-chart.git
```

2. Create a new branch
```
cd freeradius-helm-chart
git checkout -b my-awesome-config-change
```

3. Make changes in your configuration

4. Commit your changes
```
git add ./path/to/your/change
git commit -v
```

5. Push your changes to the remote branch
```
git push origin my-awesome-config-change
```

6. Wait for the build to successeed and then merge the branch. The build will validate the configuration.
7. The changes will be deployed on AWS EKS dgtek-infra-prod automatically.

## Building a new image manually (NOT RECOMMENDED) and deploying with helm

1. Login to ECR (AWS Container Registry)
```
aws ecr get-login-password --region ap-southeast-2 | docker login --username AWS --password-stdin 073068687739.dkr.ecr.ap-southeast-2.amazonaws.com
```

2. Build and push image
```
docker build -t freeradius .
docker tag freeradius:latest 073068687739.dkr.ecr.ap-southeast-2.amazonaws.com/freeradius:MY_AWESOME_TAG
docker push 073068687739.dkr.ecr.ap-southeast-2.amazonaws.com/freeradius:MY_AWESOME_TAG
```

3. Upgrade helm chart
```
cd helm/freeradius
helm upgrade  -n freeradius freeradius . --set tag=MY_AWESOME_TAG
```
