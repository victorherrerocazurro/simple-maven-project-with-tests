pipeline {
agent { docker 'maven:3-alpine' } ①
stages {
stage('Example Build') {
steps {
sh 'mvn -Dmaven.test.failure.ignore clean package'
}
}
}
}
