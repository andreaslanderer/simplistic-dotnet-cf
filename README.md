# .NET Core goes AWS Fargate

## What is this?

- Focus: an AWS CloudFormation template that allows you to run a dockerized Hello World application in ECS Fargate
- Sample workload: a simple Hello World AspNetCore app (one of my first .NET Core applications, btw.) that talks to MS SQL Server and logs in "CloudWatch Logs Insights-friendly" JSON
- A few bash scripts so that you do not have to leave the console

## AWS stuff covered

- Leverages docker to build the AspNetCore app and to build the AspNetCore app docker image
- docker push to Amazon ECR
- curl -(HTTP)-> Application Load Balancer -(HTTP)-> dockerized AspNetCore app running as a Elastic Container Service (Fargate) service -(1433)-> Amazon RDS for SQL server
- AWS Secrets Manager holds RDS credentials / connection string

## Preconditions

- Linux-like OS (e.g. macOS)
- AWS CLI v2 installed and configured (e.g. aws configure sso)
- Docker installed
- Tools for everyday use: bash, sed, curl, jq
- Optional: Visual Studio Code and .NET Core plugins installed

## Steps

VS Code:

    #./docker_run_db.sh

    F5

    open https://localhost:5001/WeatherForecast

Docker:

    ./docker_run_db.sh
    #./docker_run_db_sqlcmd.sh

    ./docker_build.sh
    ./docker_run_app.sh

    ./curl_app.sh

AWS:

    #export AWS_PROFILE=admin-hslu

    ./create_stack_ecr.sh
    ./create_stack_application.sh

    ./ecr_dockerlogin.sh
    ./docker_build.sh
    ./ecr_dockerpush.sh 

    ./update_stack_application.sh

    ./curl_stack_application.sh

    ./delete_stack_application.sh 
    ./delete_stack_ecr.sh

Enjoy!