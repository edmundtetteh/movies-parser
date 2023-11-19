// pipeline {
//     agent { label 'dev' }

//     environment {
//         imageName = 'edmundtetteh/movies-parser'
//         registry = 'https://registry.slowcoder.com'
//     }

//     stages {
//         stage('Checkout') {
//             steps {
//                 checkout([$class: 'GitSCM', branches: [[name: 'develop']],
//                           userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
//                           credentialsId: 'ubuntu-jenkins'])
//             }
//         }

//         stage('Quality Tests') {
//             steps {
//                 script {
//                     sh "docker build -t ${imageName}-test -f Dockerfile.test ."
//                     sh "docker run --rm ${imageName}-test golint"
//                 }
//             }
//         }
//     }
// }


node('dev') {
    // Define environment variable
    def imageName = 'edmundtetteh/movies-parser'
    def registry = 'https://registry.slowcoder.com'

    // Stage: Checkout
    stage('Checkout') {
        // Git checkout
        checkout([$class: 'GitSCM', branches: [[name: 'develop']],
                  userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
                  credentialsId: 'ubuntu-jenkins'])
    }

    // Stage: Quality Tests
    stage('Quality Tests') {
        // Build the Docker image
        sh "docker build -t ${imageName}-test -f Dockerfile.test ."

        // Run golint inside the Docker container
        sh "docker run --rm ${imageName}-test golint"
    }

    stage('Unit Tests'){
        // Run go test inside the Docker container
    sh "docker run --rm ${imageName}-test go test"
    }

    stage('Security Tests') {
    // Run commands inside the Docker container with a specific user
    sh "docker run -u root:root ${imageName}-test nancy /go/src/github/${imageName}/Gopkg.lock"
    }
    
}










