def imageName = 'edmundtetteh/movies-parser'
def registry = 'https://registry.slowcoder.com'

node('dev') {
    stage('Checkout') {
        checkout([$class: 'GitSCM', branches: [[name: 'develop']],
                userRemoteConfigs: [[url: 'https://github.com/edmundtetteh/movies-parser.git']],
                credentialsId: 'ubuntu-jenkins'])
    }

    def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")

    stage('Pre-integration Tests'){
        parallel(
            'Quality Tests': {
                imageTest.inside{
                    sh 'golint'
                }
            },
            'Unit Tests': {
                imageTest.inside{
                    sh 'go test'
                }
            },
            'Security Tests': {
                imageTest.inside('-u root:root'){
                    sh 'nancy /go/src/github/edmund/movies-parser/Gopkg.lock'
                }
            }
        )
}

    // Add more stage
}


