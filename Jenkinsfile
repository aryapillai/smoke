pipeline {

   agent any

   stages {

       stage('Clone Repository') {

           steps {

               git branch: 'main',
               url: 'https://github.com/aryapillai/smoke.git'

           }

       }

       stage('Build Docker Image') {

           steps {

               sh '''
               docker build -t smoke-demo .
               '''

           }

       }

       stage('Run Container') {

           steps {

               sh '''
               docker run -d --name smoke-test2 -p 8087:80 smoke-demo
               '''

           }

       }

       stage('Smoke Test') {

           steps {

               sh '''
               sleep 5

               curl http://localhost:8087
               '''

           }

       }

       stage('Cleanup') {

           steps {

               sh '''
               docker stop smoke-test2
               docker rm smoke-test2
               '''

           }

       }

   }

}
