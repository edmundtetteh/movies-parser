// def imageName = 'edmundtetteh/movies-parser'
// def registry = 'https://registry.slowcoder.com'

// node('dev') {
//     stage('Checkout') {
//         checkout([$class: 'GitSCM', branches: [[name: 'develop']],
//                 userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
//                 credentialsId: 'ubuntu-jenkins'])
//     }

//     def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

//     stage('Pre-integration Tests'){
//         parallel(
//             // 'Quality Tests': {
//             //     imageTest.inside{
//             //         sh 'golint'
//             //     }
//             // },
//         'Quality Tests': {
//         catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
//             imageTest.inside {
//                 sh 'golint'
//                 }
//             }
//         },
        

//             'Unit Tests': {
//                 imageTest.inside{
//                     sh 'go test'
//                 }
//             },
//             'Security Tests': {
//                 imageTest.inside('-u root:root'){
//                     sh 'nancy /go/src/github/edmundtetteh/movies-parser/Gopkg.lock'
//                 }
//             }
//         )
// }

//     // Add more stage
// }

// def imageName = 'edmundtetteh/movies-parser'
// def registry = 'https://registry.slowcoder.com'

// node('dev') {
//     stage('Checkout') {
//         checkout([$class: 'GitSCM', branches: [[name: 'develop']],
//                   userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
//                   credentialsId: 'ubuntu-jenkins'])
//     }


//     stage('Quality Tests'){
//        def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
//         imageTest.inside{
//             sh 'golint'
//         }
//     }
// }

pipeline {
    agent { label 'dev' }

    environment {
        imageName = 'edmundtetteh/movies-parser'
        registry = 'https://registry.slowcoder.com'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: 'develop']],
                          userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
                          credentialsId: 'ubuntu-jenkins'])
            }
        }

        stage('Quality Tests') {
            steps {
                script {
                    sh "docker build -t ${imageName}-test -f Dockerfile.test ."
                    sh "docker run --rm ${imageName}-test golint"
                }
            }
        }
    }
}




