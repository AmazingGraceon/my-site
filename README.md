on:
  push:
    branches: [ main ]
jobs:
  build_push:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id:   ${{ secrets.AWS_KEY }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET }}
          aws-region: ap-northeast-2
      - run: |
          docker build -t $ECR/sellerbot:airflow docker/airflow
          docker push $ECR/sellerbot:airflow
  helm_deploy:
    needs: build_push
    runs-on: ubuntu-latest
    steps:
      - uses: azure/setup-helm@v4
      - run: |
          helm upgrade --install sbot kubernetes/helm-chart \
            --set image.tag=airflow

